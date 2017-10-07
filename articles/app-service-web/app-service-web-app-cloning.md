---
title: "aaaWeb приложения клонирование, с помощью PowerShell"
description: "Узнайте, как tooclone веб-приложения toonew веб-приложений с помощью PowerShell."
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
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="8cf5c-103">Клонирование приложений службы приложений Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8cf5c-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="8cf5c-104">С выпуском Microsoft Azure PowerShell hello версии 1.1.0 был добавлен новый параметр добавлен tooNew AzureRMWebApp, который предоставит hello пользователя hello возможность tooclone существующего приложения tooa только что созданный веб-приложения в другой регион или hello одного региона.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="8cf5c-105">Это позволит клиентам toodeploy количество приложений в разных регионах быстро и легко.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="8cf5c-106">В настоящее время клонирование приложений поддерживается только в планах службы приложений уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="8cf5c-107">новый компонент использует Hello hello же ограничения, как средство резервного копирования приложений Web, в разделе [резервное копирование веб-приложения в службе приложений Azure](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="8cf5c-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="8cf5c-108">toolearn об использовании диспетчера ресурсов Azure на основе toomanage командлеты Azure PowerShell возврат веб-приложений [диспетчера ресурсов Azure на основе команд PowerShell для веб-приложения Azure](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8cf5c-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="8cf5c-109">Клонирование существующего приложения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-109">Cloning an existing App</span></span>
<span data-ttu-id="8cf5c-110">Сценарий: Существующий веб-приложение в регионе США, hello пользователь предпочитает tooclone hello содержимое tooa новое веб-приложение в Центре области.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="8cf5c-111">Это можно сделать с помощью версии диспетчера ресурсов Azure hello toocreate командлет PowerShell hello новое веб-приложение с параметром - SourceWebApp hello.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="8cf5c-112">Зная ресурсов hello имя группы, которое содержит hello исходного веб-приложения, можно использовать следующую информацию PowerShell команды tooget hello источника веб-приложения (в данном случае с именем источника webapp) hello:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="8cf5c-113">toocreate новый план служб приложений, можно использовать команду New-AzureRmAppServicePlan как следующий пример hello</span><span class="sxs-lookup"><span data-stu-id="8cf5c-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="8cf5c-114">С помощью команды New-AzureRmWebApp hello, мы можно создать новое веб-приложение hello в регионе hello North Central US и привязать tooan план служб приложений существующего уровня premium, кроме того, мы используем hello того же ресурса группу, что hello исходного веб-приложения, или определить новую группу ресурсов , hello ниже показано, что:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="8cf5c-115">tooclone существующего веб-приложения, включая все слоты развертывания связанных, hello пользователю будет необходимо toouse Здравствуйте параметр IncludeSourceWebAppSlots, hello следующую команду PowerShell показано использование этого параметра с помощью команды New-AzureRmWebApp hello hello:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="8cf5c-116">tooclone существующего веб-приложения, в пределах hello же регионе hello пользователю будет необходимо toocreate план новую группу ресурсов и новую службу приложения hello же регионе, а затем с помощью hello следующие PowerShell команды tooclone hello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="8cf5c-117">Клонирование существующих приложений tooan среды службы приложений</span><span class="sxs-lookup"><span data-stu-id="8cf5c-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="8cf5c-118">Сценарий: Существующий веб-приложение в регионе США, hello пользователь предпочитает tooclone hello содержимое tooa новый web app tooan существующие среды службы приложений (ASE).</span><span class="sxs-lookup"><span data-stu-id="8cf5c-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="8cf5c-119">Зная ресурсов hello имя группы, которое содержит hello исходного веб-приложения, можно использовать следующую информацию PowerShell команды tooget hello источника веб-приложения (в данном случае с именем источника webapp) hello:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="8cf5c-120">Необходимо знать имя hello ASE и имя группы ресурсов hello, к которой принадлежит hello ASE, hello пользователя можно использовать команду New AzureRmWebApp hello что toocreate hello новое веб-приложение в существующий ASE hello, следуя hello демонстрирует, что:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="8cf5c-121">Параметр расположения Hello требуется из-за причин toolegacy, однако в случае hello при создании приложения в ASE оно будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="8cf5c-122">Клонирование существующего слота приложения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="8cf5c-123">Сценарий: hello пользователь предпочитает tooclone существующих приложений гнездо Web tooeither новое веб-приложение или новая область веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="8cf5c-124">новое веб-приложение может быть в hello Hello же регионе, как исходный слот веб-приложения hello, или в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="8cf5c-125">Зная ресурсов hello имя группы, которое содержит hello исходного веб-приложения, можно использовать следующую команду PowerShell tooget hello источника web app слота сведения (в данном случае с именем источника webappslot) привязан tooWeb приложения источника-веб-приложение hello:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="8cf5c-126">Hello следующий код демонстрирует создание клона hello исходного web app tooa нового веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="8cf5c-127">Настройка диспетчера трафика при клонировании приложения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="8cf5c-128">Создание нескольких регионах веб-приложений и настройки диспетчера трафика Azure tooroute трафика tooall этих веб-приложений, tooinsure n важные сценарии, заказчиков приложений высокой надежности при клонировании существующего веб-приложения, которым у вас есть hello tooconnect параметр обоих веб tooeither приложений нового профиля диспетчера трафика или уже существующей - Обратите внимание, что только версия диспетчера ресурсов Azure поддерживается диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="8cf5c-129">Создание нового профиля диспетчера трафика при клонировании приложения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="8cf5c-130">Сценарий: hello пользователь предпочитает tooclone область tooanother web app, при настройке профиля диспетчера трафика Azure Resource Manager, среди оба веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="8cf5c-131">Hello следующий код демонстрирует создание клона hello источника web app tooa новое веб-приложение при настройке профиля диспетчера трафика:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="8cf5c-132">Добавление нового клонированного веб-приложения tooan существующего профиля диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="8cf5c-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="8cf5c-133">Сценарий: hello пользователя уже есть профиль диспетчера трафика Azure Resource Manager, он хотел tooadd веб-приложения в качестве конечных точек.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="8cf5c-134">toodo таким образом, необходимо сначала tooassemble Здравствуйте, существующий код профиля диспетчера трафика, нам нужно будет hello идентификатор подписки, имя группы ресурсов и hello трафика manager имени существующего профиля.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="8cf5c-135">После того, идентификатор диспетчера трафика hello, hello следующий код демонстрирует создание клона hello исходного web app tooa нового веб-приложения во время добавления их tooan существующего профиля диспетчера трафика:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="8cf5c-136">Существующие ограничения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-136">Current Restrictions</span></span>
<span data-ttu-id="8cf5c-137">Эта функция в настоящее время находится в предварительной версии, со временем мы работаем tooadd новые возможности, hello после списка являются hello известные ограничения в текущей версии hello клонирования приложения:</span><span class="sxs-lookup"><span data-stu-id="8cf5c-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="8cf5c-138">Параметры автоматического масштабирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="8cf5c-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="8cf5c-139">Параметры расписания резервного копирования не клонируются</span><span class="sxs-lookup"><span data-stu-id="8cf5c-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="8cf5c-140">Параметры виртуальных сетей не клонируются</span><span class="sxs-lookup"><span data-stu-id="8cf5c-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="8cf5c-141">Подробные сведения о приложении не настраиваются автоматически на веб-приложения hello назначения</span><span class="sxs-lookup"><span data-stu-id="8cf5c-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="8cf5c-142">Параметры простой авторизации не клонируются</span><span class="sxs-lookup"><span data-stu-id="8cf5c-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="8cf5c-143">Расширение Kudu не клонируется</span><span class="sxs-lookup"><span data-stu-id="8cf5c-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="8cf5c-144">Правила TiP не клонируются</span><span class="sxs-lookup"><span data-stu-id="8cf5c-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="8cf5c-145">Содержимое базы данных не клонируется.</span><span class="sxs-lookup"><span data-stu-id="8cf5c-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="8cf5c-146">Ссылки</span><span class="sxs-lookup"><span data-stu-id="8cf5c-146">References</span></span>
* [<span data-ttu-id="8cf5c-147">Команды Azure PowerShell на основе Azure Resource Manager для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="8cf5c-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="8cf5c-148">Клонирование веб-приложения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8cf5c-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="8cf5c-149">Резервное копирование веб-приложений в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="8cf5c-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="8cf5c-150">Предварительная поддержка диспетчера трафика Azure в диспетчере ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="8cf5c-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="8cf5c-151">Введение tooApp среды службы</span><span class="sxs-lookup"><span data-stu-id="8cf5c-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="8cf5c-152">Использование Azure PowerShell с диспетчером ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="8cf5c-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

