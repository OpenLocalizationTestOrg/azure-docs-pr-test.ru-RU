---
title: "Клонирование веб-приложения с помощью PowerShell"
description: "Узнайте, как клонировать веб-приложения, создавая новые веб-приложения, с помощью PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="e5763-103">Клонирование приложений службы приложений Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5763-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="e5763-104">С выходом Microsoft Azure PowerShell версии 1.1.0 в командлет New-AzureRMWebApp был добавлен новый параметр, позволяющий пользователю клонировать существующее веб-приложение во вновь созданное приложение, размещенное в том же или в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="e5763-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new option has been added to New-AzureRMWebApp that would give the user the ability to clone an existing Web App to a newly created app in a different region or in the same region.</span></span> <span data-ttu-id="e5763-105">Так пользователи смогут легко и быстро развернуть целый ряд приложений в различных регионах.</span><span class="sxs-lookup"><span data-stu-id="e5763-105">This will enable customers to deploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="e5763-106">В настоящее время клонирование приложений поддерживается только в планах службы приложений уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="e5763-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="e5763-107">В новой функции действуют те же ограничения, что и в функции архивации веб-приложений (см. статью [Резервное копирование веб-приложений в службе приложений Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="e5763-107">The new feature uses the same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="e5763-108">Дополнительные сведения об использовании командлетов Azure PowerShell на основе Azure Resource Manager для управления веб-приложениями см. [здесь](app-service-web-app-azure-resource-manager-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e5763-108">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="e5763-109">Клонирование существующего приложения</span><span class="sxs-lookup"><span data-stu-id="e5763-109">Cloning an existing App</span></span>
<span data-ttu-id="e5763-110">Сценарий: существует веб-приложение в южно-центральном регионе США; пользователь хотел бы клонировать его содержимое в новое веб-приложение в северо-центральном регионе США.</span><span class="sxs-lookup"><span data-stu-id="e5763-110">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app in North Central US region.</span></span> <span data-ttu-id="e5763-111">Эту задачу можно решить с помощью командлета PowerShell на основе Azure Resource Manager для создания веб-приложения с параметром SourceWebApp.</span><span class="sxs-lookup"><span data-stu-id="e5763-111">This can be accomplished by using the Azure Resource Manager version of the PowerShell cmdlet to create a new web app with the -SourceWebApp option.</span></span>

<span data-ttu-id="e5763-112">Зная имя группы ресурсов, содержащей исходное веб-приложение, мы можем выполнить следующую команду PowerShell для получения данных исходного веб-приложения (в данном случае оно называется source-webapp):</span><span class="sxs-lookup"><span data-stu-id="e5763-112">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="e5763-113">Чтобы создать новый план службы приложений, можно выполнить команду New-AzureRmAppServicePlan, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e5763-113">To create a new App Service Plan, we can use New-AzureRmAppServicePlan command as in the following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="e5763-114">С помощью команды New-AzureRmWebApp можно создать новое веб-приложение в северо-центральном регионе США и привязать его к существующему плану службы приложений уровня Premium. Более того, можно использовать в качестве исходного веб-приложения ту же группу ресурсов или определить новую:</span><span class="sxs-lookup"><span data-stu-id="e5763-114">Using the New-AzureRmWebApp command, we can create the new web app in the North Central US region, and tie it to an existing premium tier App Service Plan, moreover we can use the same resource group as the source web app, or define a new resource group, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="e5763-115">Для создания точной копии существующего веб-приложения, включая все соответствующие слоты развертывания, пользователю необходимо будет задать параметр IncludeSourceWebAppSlots. Следующая команда PowerShell показывает, как использовать этот параметр с командой New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="e5763-115">To clone an existing web app including all associated deployment slots, the user will need to use the IncludeSourceWebAppSlots parameter, the following PowerShell command demonstrates the use of that parameter with the New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="e5763-116">Для создания точной копии существующего веб-приложения в том же регионе пользователю нужно будет создать новую группу ресурсов и новый план службы приложений в том же регионе, а затем клонировать веб-приложение с помощью следующей команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e5763-116">To clone an existing web app within the same region, the user will need to create a new resource group and a new app service plan in the same region, and then using the following PowerShell command to clone the web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a><span data-ttu-id="e5763-117">Клонирование существующего приложения в среду службы приложений</span><span class="sxs-lookup"><span data-stu-id="e5763-117">Cloning an existing App to an App Service Environment</span></span>
<span data-ttu-id="e5763-118">Сценарий: существует веб-приложение в южно-центральном регионе США; пользователь хотел бы клонировать его содержимое в новое веб-приложение в существующую среду службы приложений (ASE).</span><span class="sxs-lookup"><span data-stu-id="e5763-118">Scenario: An existing web app in South Central US region, the user would like to clone the contents to a new web app to an existing App Service Environment (ASE).</span></span>

<span data-ttu-id="e5763-119">Зная имя группы ресурсов, содержащей исходное веб-приложение, мы можем выполнить следующую команду PowerShell для получения данных исходного веб-приложения (в данном случае оно называется source-webapp):</span><span class="sxs-lookup"><span data-stu-id="e5763-119">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="e5763-120">Зная имя ASE и имя группы ресурсов, к которой относится ASE, пользователь может создать новое веб-приложение в существующей ASE, выполнив следующую команду New-AzureRmWebApp:</span><span class="sxs-lookup"><span data-stu-id="e5763-120">Knowing the ASE's name, and the resource group name that the ASE belongs to, the user can use the New-AzureRmWebApp command to create the new web app in the existing ASE, the following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="e5763-121">В связи с обратной совместимостью параметр Location является обязательным, однако при создании приложения в ASE он игнорируется.</span><span class="sxs-lookup"><span data-stu-id="e5763-121">The Location parameter is required due to legacy reason, but in the case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="e5763-122">Клонирование существующего слота приложения</span><span class="sxs-lookup"><span data-stu-id="e5763-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="e5763-123">Сценарий: пользователь хочет клонировать существующий слот веб-приложения в новое веб-приложение или в новый слот веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e5763-123">Scenario: The user would like to clone an existing Web App Slot to either a new Web App or a new Web App slot.</span></span> <span data-ttu-id="e5763-124">Новое веб-приложение может размещаться в том же регионе, что и исходный слот, или в другом.</span><span class="sxs-lookup"><span data-stu-id="e5763-124">The new Web App can be in the same region as the original Web App slot or in a different region.</span></span>

<span data-ttu-id="e5763-125">Зная имя группы ресурсов, содержащей исходное веб-приложение, мы можем выполнить следующую команду PowerShell для получения данных исходного слота веб-приложения (в данном случае оно называется source-webappslot), привязанного к веб-приложению source-webappslot:</span><span class="sxs-lookup"><span data-stu-id="e5763-125">Knowing the resource group name that contains the source web app, we can use the following PowerShell command to get the source web app slot's information (in this case named source-webappslot) tied to Web App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="e5763-126">Следующая команда демонстрирует создание точной копии исходного веб-приложения в новом веб-приложении:</span><span class="sxs-lookup"><span data-stu-id="e5763-126">The following demonstrates creating a clone of the source web app to a new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="e5763-127">Настройка диспетчера трафика при клонировании приложения</span><span class="sxs-lookup"><span data-stu-id="e5763-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="e5763-128">Создание мультирегиональных веб-приложений и настройка в диспетчере трафика Azure маршрутизации трафика ко всем этим веб-приложениям — это важный сценарий, обеспечивающий высокую доступность приложений клиентов. Клонируя существующее веб-приложение, вы можете подключить оба веб-приложения к новому или существующему профилю диспетчера трафика. Обратите внимание, что поддерживается только версия диспетчера трафика на основе Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5763-128">Creating multi-region web apps and configuring Azure Traffic Manager to route traffic to all these web apps, is a n important scenario to insure that customers' apps are highly available, when cloning an existing web app you have the option to connect both web apps to either a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="e5763-129">Создание нового профиля диспетчера трафика при клонировании приложения</span><span class="sxs-lookup"><span data-stu-id="e5763-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="e5763-130">Сценарий: пользователь хочет клонировать веб-приложение в другой регион и настроить профиль диспетчера трафика Azure Resource Manager так, чтобы он включал оба веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e5763-130">Scenario: The user would like to clone an web app to another region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="e5763-131">Следующая команда демонстрирует создание точной копии исходного веб-приложения в новом веб-приложении с настройкой нового профиля диспетчера трафика:</span><span class="sxs-lookup"><span data-stu-id="e5763-131">The following demonstrates creating a clone of the source web app to a new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a><span data-ttu-id="e5763-132">Добавление клонированного веб-приложения в существующий профиль диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="e5763-132">Adding new cloned Web App to an existing Traffic Manager profile</span></span>
<span data-ttu-id="e5763-133">Сценарий: у пользователя уже есть профиль диспетчера трафика Azure Resource Manager, и он хотел бы добавить оба веб-приложения в качестве конечных точек.</span><span class="sxs-lookup"><span data-stu-id="e5763-133">Scenario: The user already have an Azure Resource Manager traffic manager profile that he would like to add both web apps as endpoints.</span></span> <span data-ttu-id="e5763-134">Для этого нужно знать идентификатор профиля диспетчера трафика, идентификатор подписки, имя группы ресурсов и имя существующего профиля диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="e5763-134">To do so, we first need to assemble the existing traffic manager profile id, we will need the subscription id, resource group name and the existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="e5763-135">Следующая команда показывает, как создать точную копию исходного веб-приложения в новом веб-приложении и добавить эти веб-приложения в существующий профиль диспетчера трафика, зная идентификатор диспетчер трафика:</span><span class="sxs-lookup"><span data-stu-id="e5763-135">After having the traffic manger id, the following demonstrates creating a clone of the source web app to a new web app while adding them to an existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="e5763-136">Существующие ограничения</span><span class="sxs-lookup"><span data-stu-id="e5763-136">Current Restrictions</span></span>
<span data-ttu-id="e5763-137">В настоящее время эта функция доступна в режиме предварительной версии, и со временем ее возможности будут расширены. В текущей версии функции клонирования приложений существуют следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="e5763-137">This feature is currently in preview, we are working to add new capabilities over time, the following list are the known restrictions on the current version of app cloning:</span></span>

* <span data-ttu-id="e5763-138">Параметры автоматического масштабирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="e5763-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="e5763-139">Параметры расписания резервного копирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="e5763-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="e5763-140">Параметры виртуальных сетей не клонируются</span><span class="sxs-lookup"><span data-stu-id="e5763-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="e5763-141">App Insights не настраивается в целевом веб-приложении автоматически</span><span class="sxs-lookup"><span data-stu-id="e5763-141">App Insights are not automatically set up on the destination web app</span></span>
* <span data-ttu-id="e5763-142">Параметры простой авторизации не клонируются</span><span class="sxs-lookup"><span data-stu-id="e5763-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="e5763-143">Расширение Kudu не клонируется</span><span class="sxs-lookup"><span data-stu-id="e5763-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="e5763-144">Правила TiP не клонируются</span><span class="sxs-lookup"><span data-stu-id="e5763-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="e5763-145">Содержимое базы данных не клонируется.</span><span class="sxs-lookup"><span data-stu-id="e5763-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="e5763-146">Ссылки</span><span class="sxs-lookup"><span data-stu-id="e5763-146">References</span></span>
* [<span data-ttu-id="e5763-147">Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e5763-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="e5763-148">Клонирование веб-приложения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e5763-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="e5763-149">Резервное копирование веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e5763-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="e5763-150">Предварительная поддержка диспетчера трафика Azure в диспетчере ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e5763-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="e5763-151">Введение в среду службы приложения</span><span class="sxs-lookup"><span data-stu-id="e5763-151">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="e5763-152">Использование Azure PowerShell с диспетчером ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e5763-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

