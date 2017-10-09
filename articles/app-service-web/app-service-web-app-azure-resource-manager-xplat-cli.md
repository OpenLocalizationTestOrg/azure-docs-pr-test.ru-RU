---
title: "aaaAzure диспетчер ресурсов на основе кросс платформенных средства командной строки для веб-приложения Azure | Документы Microsoft"
description: "Узнайте, как toouse hello новый toomanage диспетчера ресурсов Azure кросс платформенных командной строки средства на основе веб-приложения Azure."
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
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a><span data-ttu-id="4d584-103">Использование кроссплатформенного интерфейса командной строки на основе Azure Resource Manager для службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4d584-103">Using Azure Resource Manager-Based XPlat CLI for Azure App Service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d584-104">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="4d584-104">Azure CLI</span></span>](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [<span data-ttu-id="4d584-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d584-105">Azure PowerShell</span></span>](app-service-web-app-azure-resource-manager-powershell.md)

<span data-ttu-id="4d584-106">В выпуске версии средств командной строки Microsoft Azure кросс платформенных 0.10.5 hello были добавлены новые команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-106">With hello release of Microsoft Azure Cross-platform Command-Line Tools version 0.10.5, new commands have been added.</span></span> <span data-ttu-id="4d584-107">Эти команды дают toomanage под управлением диспетчера ресурсов Azure PowerShell команды hello возможность hello пользователя toouse службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4d584-107">These commands give hello user hello ability toouse Azure Resource Manager-based PowerShell commands toomanage App Service.</span></span>

<span data-ttu-id="4d584-108">toolearn об управлении группами ресурсов, в разделе [toomanage Azure CLI hello Azure использовать ресурсы и группы ресурсов](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4d584-108">toolearn about managing Resource Groups, see [Use hello Azure CLI toomanage Azure resources and resource groups](../azure-resource-manager/xplat-cli-azure-resource-manager.md).</span></span> 

> [!NOTE] 
> <span data-ttu-id="4d584-109">Кроме того, попробуйте [Azure CLI 2.0](https://github.com/Azure/azure-cli), CLI следующего поколения, языке Python для модели развертывания hello ресурса управления.</span><span class="sxs-lookup"><span data-stu-id="4d584-109">Also, try out [Azure CLI 2.0](https://github.com/Azure/azure-cli), a next-generation CLI written in Python for hello resource management deployment model.</span></span>
>
>

## <a name="managing-app-service-plans"></a><span data-ttu-id="4d584-110">Управление планами службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-110">Managing App Service Plans</span></span>
### <a name="create-an-app-service-plan"></a><span data-ttu-id="4d584-111">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-111">Create an App Service Plan</span></span>
<span data-ttu-id="4d584-112">toocreate план служб приложений использовать hello **создания azure appserviceplan** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-112">toocreate an app service plan, use hello **azure appserviceplan create** command.</span></span>

<span data-ttu-id="4d584-113">Ниже описаны различные параметры hello:</span><span class="sxs-lookup"><span data-stu-id="4d584-113">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="4d584-114">**--группы ресурсов**: группа ресурсов, содержащая hello только что созданный план обслуживания приложений.</span><span class="sxs-lookup"><span data-stu-id="4d584-114">**--resource-group**: resource group that includes hello newly created app service plan.</span></span>
* <span data-ttu-id="4d584-115">**— имя**: имя плана обслуживания приложений hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-115">**--name**: name of hello app service plan.</span></span>
* <span data-ttu-id="4d584-116">**--location**: расположение плана службы.</span><span class="sxs-lookup"><span data-stu-id="4d584-116">**--location**: app service plan location.</span></span>
* <span data-ttu-id="4d584-117">**--sku**: hello требуемого ценообразования sku (параметры hello: F1 (Free).</span><span class="sxs-lookup"><span data-stu-id="4d584-117">**--sku**:  hello desired pricing sku (hello options are: F1 (Free).</span></span> <span data-ttu-id="4d584-118">Варианты: F1 (бесплатный); D1 (общедоступный);</span><span class="sxs-lookup"><span data-stu-id="4d584-118">D1 (Shared).</span></span> <span data-ttu-id="4d584-119">B1 (малый базовый), B2 (средний базовый) и B3 (крупный базовый);</span><span class="sxs-lookup"><span data-stu-id="4d584-119">B1 (Basic Small), B2 (Basic Medium), and B3 (Basic Large).</span></span> <span data-ttu-id="4d584-120">S1 (малый стандартный), S2 (средний стандартный) и S3 (крупный стандартный);</span><span class="sxs-lookup"><span data-stu-id="4d584-120">S1 (Standard Small), S2 (Standard Medium), and S3 (Standard Large).</span></span> <span data-ttu-id="4d584-121">P1 (малый премиум), P2 (средний премиум) и P3 (крупный премиум).</span><span class="sxs-lookup"><span data-stu-id="4d584-121">P1 (Premium Small), P2 (Premium Medium), and P3 (Premium Large).)</span></span>
* <span data-ttu-id="4d584-122">**--экземпляров**: hello число рабочих процессов в hello плана (значение по умолчанию — 1).</span><span class="sxs-lookup"><span data-stu-id="4d584-122">**--instances**: hello number of workers in hello app service plan (Default value is 1).</span></span>

<span data-ttu-id="4d584-123">Пример toouse этого командлета:</span><span class="sxs-lookup"><span data-stu-id="4d584-123">Example toouse this cmdlet:</span></span>

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="4d584-124">Создание плана службы приложений Linux</span><span class="sxs-lookup"><span data-stu-id="4d584-124">Create a Linux App Service Plan</span></span>

<span data-ttu-id="4d584-125">С помощью hello же **создания azure appserviceplan** команду с hello дополнительный параметр **true--islinux**.</span><span class="sxs-lookup"><span data-stu-id="4d584-125">Using hello same **azure appserviceplan create** command, with hello extra parameter **--islinux true**.</span></span> <span data-ttu-id="4d584-126">Обратите внимание на ограничения hello и областей, описанные в [tooApp введение службы в Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4d584-126">Note hello restrictions and regions outlined in [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>

### <a name="list-existing-app-service-plans"></a><span data-ttu-id="4d584-127">Получение списка существующих планов службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-127">List Existing App Service Plans</span></span>
<span data-ttu-id="4d584-128">использовать toolist hello существующих планах службы приложений, **список azure appserviceplan** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-128">toolist hello existing app service plans, use **azure appserviceplan list** command.</span></span>

<span data-ttu-id="4d584-129">toolist всех планах службы приложений в определенной группе ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="4d584-129">toolist all app service plans under a specific resource group, use:</span></span>

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="4d584-130">использовать tooget план обслуживания определенного приложения **Показать azure appserviceplan** команды:</span><span class="sxs-lookup"><span data-stu-id="4d584-130">tooget a specific app service plan, use **azure appserviceplan show** command:</span></span>

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a><span data-ttu-id="4d584-131">Настройка существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-131">Configure an existing App Service Plan</span></span>
<span data-ttu-id="4d584-132">Параметры hello toochange существующего плана служб приложений, используйте hello **конфигурации azure appserviceplan** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-132">toochange hello settings for an existing app service plan, use hello **azure appserviceplan config** command.</span></span> <span data-ttu-id="4d584-133">Вы можете изменить hello sku и hello число рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="4d584-133">You can change hello sku, and hello number of workers</span></span> 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a><span data-ttu-id="4d584-134">Масштабирование плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-134">Scaling an App Service Plan</span></span>
<span data-ttu-id="4d584-135">использовать существующий план служб приложений, tooscale:</span><span class="sxs-lookup"><span data-stu-id="4d584-135">tooscale an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a><span data-ttu-id="4d584-136">Изменение hello SKU план служб приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-136">Changing hello SKU of an App Service Plan</span></span>
<span data-ttu-id="4d584-137">toochange sku hello существующий план служб приложений, используйте:</span><span class="sxs-lookup"><span data-stu-id="4d584-137">toochange hello sku of an existing App Service Plan, use:</span></span>

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a><span data-ttu-id="4d584-138">Удаление существующего плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-138">Delete an existing App Service Plan</span></span>
<span data-ttu-id="4d584-139">toodelete существующего плана служб приложений все назначенные приложений необходимость toobe перемещен или удален сначала.</span><span class="sxs-lookup"><span data-stu-id="4d584-139">toodelete an existing app service plan, all assigned apps need toobe moved or deleted first.</span></span> <span data-ttu-id="4d584-140">Затем с помощью hello **удалить azure веб-приложение** команды, вы можете удалить план служб приложений hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-140">Then using hello **azure webapp delete** command you can delete hello app service plan.</span></span>

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a><span data-ttu-id="4d584-141">Управление приложениями службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-141">Managing App Service apps</span></span>
### <a name="create-a-web-app"></a><span data-ttu-id="4d584-142">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-142">Create a web app</span></span>
<span data-ttu-id="4d584-143">toocreate веб-приложения, используйте hello **azure веб-приложения создайте** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-143">toocreate a web app, use hello **azure webapp create** command.</span></span>

<span data-ttu-id="4d584-144">Ниже описаны различные параметры hello:</span><span class="sxs-lookup"><span data-stu-id="4d584-144">Following are descriptions of hello different parameters:</span></span>

* <span data-ttu-id="4d584-145">**— имя**: имя для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-145">**--name**: name for hello web app.</span></span>
* <span data-ttu-id="4d584-146">**--плана**: имя для плана обслуживания hello используется toohost hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4d584-146">**--plan**: name for hello service plan used toohost hello web app.</span></span>
* <span data-ttu-id="4d584-147">**--группы ресурсов**: группы ресурсов, на котором размещена hello план обслуживания приложений.</span><span class="sxs-lookup"><span data-stu-id="4d584-147">**--resource-group**: resource group that hosts hello App service plan.</span></span>
* <span data-ttu-id="4d584-148">**--расположение**: hello местоположению веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4d584-148">**--location**: hello web app location.</span></span>

<span data-ttu-id="4d584-149">Пример toouse этого командлета:</span><span class="sxs-lookup"><span data-stu-id="4d584-149">Example toouse this cmdlet:</span></span>

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a><span data-ttu-id="4d584-150">Удаление существующего приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-150">Delete an existing app</span></span>
<span data-ttu-id="4d584-151">toodelete существующего приложения, можно использовать hello **удалить azure веб-приложение** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-151">toodelete an existing app, you can use hello **azure webapp delete** command.</span></span> <span data-ttu-id="4d584-152">Требуется имя hello toospecify приложение hello и имя группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-152">You need toospecify hello name of hello app and hello resource group name.</span></span>

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a><span data-ttu-id="4d584-153">Список существующих приложений</span><span class="sxs-lookup"><span data-stu-id="4d584-153">List existing apps</span></span>
<span data-ttu-id="4d584-154">использовать существующие приложения hello toolist hello **список azure веб-приложение** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-154">toolist hello existing apps, use hello **azure webapp list** command.</span></span>

<span data-ttu-id="4d584-155">все приложения в определенной группе ресурсов, toolist использовать:</span><span class="sxs-lookup"><span data-stu-id="4d584-155">toolist all apps in a specific resource group, use:</span></span>

    azure webapp list --resource-group ContosoAzureResourceGroup

<span data-ttu-id="4d584-156">использовать tooget определенное приложение hello **Показать azure веб-приложение** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-156">tooget a specific app, use hello **azure webapp show** command.</span></span>

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a><span data-ttu-id="4d584-157">Настройка существующего приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-157">Configure an existing app</span></span>
<span data-ttu-id="4d584-158">Параметры toochange hello и конфигурации для существующего приложения, используйте hello **набор параметров конфигурации azure веб-приложение** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-158">toochange hello settings and configurations for an existing app, use hello **azure webapp config set** command.</span></span>

<span data-ttu-id="4d584-159">Пример (1): изменение hello php версии приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-159">Example (1): change hello php version of a app</span></span> 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

<span data-ttu-id="4d584-160">Пример 2. Добавление или изменение параметров приложения:</span><span class="sxs-lookup"><span data-stu-id="4d584-160">Example (2): add or change app settings</span></span>

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

<span data-ttu-id="4d584-161">другие конфигурации, которые можно изменять, tooknow hello используйте **набора конфигурации azure webapp -h** команды.</span><span class="sxs-lookup"><span data-stu-id="4d584-161">tooknow what other configuration can be changed, use hello **azure webapp config set -h** command.</span></span>

### <a name="change-hello-state-of-an-existing-app"></a><span data-ttu-id="4d584-162">Изменить состояние hello существующего приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-162">Change hello state of an existing app</span></span>
#### <a name="restart-an-app"></a><span data-ttu-id="4d584-163">Перезапуск приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-163">Restart an app</span></span>
<span data-ttu-id="4d584-164">toorestart приложения необходимо указать hello имя и группе ресурсов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-164">toorestart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a><span data-ttu-id="4d584-165">Остановка приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-165">Stop an app</span></span>
<span data-ttu-id="4d584-166">toostop приложения необходимо указать hello имя и группе ресурсов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-166">toostop an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a><span data-ttu-id="4d584-167">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-167">Start an app</span></span>
<span data-ttu-id="4d584-168">toostart приложения необходимо указать hello имя и группе ресурсов приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4d584-168">toostart an app, you must specify hello name and resource group of hello app.</span></span>

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a><span data-ttu-id="4d584-169">Управление профилями публикации приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-169">Manage publishing profiles of an app</span></span>
<span data-ttu-id="4d584-170">Каждое приложение имеет профиль публикации, который можно использовать toopublish кода.</span><span class="sxs-lookup"><span data-stu-id="4d584-170">Each app has a publishing profile that can be used toopublish your code.</span></span>

#### <a name="get-publishing-profile"></a><span data-ttu-id="4d584-171">Получение профиля публикации</span><span class="sxs-lookup"><span data-stu-id="4d584-171">Get Publishing Profile</span></span>
<span data-ttu-id="4d584-172">tooget hello профиль приложения, используйте для публикации:</span><span class="sxs-lookup"><span data-stu-id="4d584-172">tooget hello publishing profile for a app, use:</span></span>

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

<span data-ttu-id="4d584-173">Эта команда отображает hello публикации профиль имени пользователя и пароля toohello командной строки.</span><span class="sxs-lookup"><span data-stu-id="4d584-173">This command echoes hello publishing profile username and password toohello command line.</span></span>

### <a name="manage-app-hostnames"></a><span data-ttu-id="4d584-174">Управление именами узлов приложения</span><span class="sxs-lookup"><span data-stu-id="4d584-174">Manage app hostnames</span></span>
<span data-ttu-id="4d584-175">использовать toomanage привязки имени узла для вашего приложения hello **имена узлов azure webapp config** команды</span><span class="sxs-lookup"><span data-stu-id="4d584-175">toomanage hostname bindings for your app, use hello **azure webapp config hostnames** command</span></span>  

#### <a name="list-hostname-bindings"></a><span data-ttu-id="4d584-176">Список привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="4d584-176">List hostname bindings</span></span>
<span data-ttu-id="4d584-177">tooget hello текущие имя узла привязки для приложения, используйте:</span><span class="sxs-lookup"><span data-stu-id="4d584-177">tooget hello current hostname bindings for an app, use:</span></span>

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a><span data-ttu-id="4d584-178">Добавление привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="4d584-178">Add hostname bindings</span></span>
<span data-ttu-id="4d584-179">приложение tooan привязки имени узла tooadd, использование</span><span class="sxs-lookup"><span data-stu-id="4d584-179">tooadd hostname bindings tooan app, use:</span></span>

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a><span data-ttu-id="4d584-180">Удаление привязок имен узлов</span><span class="sxs-lookup"><span data-stu-id="4d584-180">Delete hostname bindings</span></span>
<span data-ttu-id="4d584-181">toodelete привязки имени узла, используйте:</span><span class="sxs-lookup"><span data-stu-id="4d584-181">toodelete hostname bindings, use:</span></span>

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a><span data-ttu-id="4d584-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d584-182">Next Steps</span></span>
* <span data-ttu-id="4d584-183">toolearn о поддержке диспетчера ресурсов Azure CLI. в разделе [toomanage Azure CLI hello Azure используйте ресурсы и группы ресурсов.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="4d584-183">toolearn about Azure Resource Manager CLI support, see [Use hello Azure CLI toomanage Azure resources and resource groups.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)</span></span>
* <span data-ttu-id="4d584-184">toolearn об управлении службы приложений с помощью PowerShell, в разделе [tooManage Using Azure Resource Manager-Based PowerShell веб-приложения Azure.](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4d584-184">toolearn about managing App Service using PowerShell, see [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)</span></span>
* <span data-ttu-id="4d584-185">в разделе toolearn о службе приложений Azure в Linux, [tooApp введение службы в Linux](app-service-linux-intro.md)</span><span class="sxs-lookup"><span data-stu-id="4d584-185">toolearn about Azure App Service on Linux, see [Introduction tooApp Service on Linux](app-service-linux-intro.md)</span></span>
