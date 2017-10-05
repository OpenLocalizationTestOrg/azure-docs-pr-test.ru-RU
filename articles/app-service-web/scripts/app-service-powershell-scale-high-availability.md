---
title: "Пример сценария Azure PowerShell. Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для глобального масштабирования веб-приложения с помощью высокодоступной архитектуры."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="56032-103">Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры</span><span class="sxs-lookup"><span data-stu-id="56032-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="56032-104">В этом сценарии вы создадите группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="56032-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="56032-105">Завершив его, вы получите высокодоступную архитектуру, обеспечивающую глобальную доступность веб-приложения на основе минимальной задержки сети.</span><span class="sxs-lookup"><span data-stu-id="56032-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="56032-106">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="56032-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="56032-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="56032-107">Sample script</span></span>

<span data-ttu-id="56032-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры")]</span><span class="sxs-lookup"><span data-stu-id="56032-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="56032-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="56032-109">Clean up deployment</span></span> 

<span data-ttu-id="56032-110">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="56032-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="56032-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="56032-111">Script explanation</span></span>

<span data-ttu-id="56032-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="56032-112">This script uses the following commands.</span></span> <span data-ttu-id="56032-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="56032-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="56032-114">Команда</span><span class="sxs-lookup"><span data-stu-id="56032-114">Command</span></span> | <span data-ttu-id="56032-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="56032-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="56032-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="56032-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="56032-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="56032-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="56032-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="56032-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="56032-119">Создает профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="56032-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="56032-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="56032-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="56032-121">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="56032-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="56032-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="56032-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="56032-123">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="56032-123">Creates a web app.</span></span> |
| [<span data-ttu-id="56032-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="56032-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="56032-125">Создает конечную точку в профиле диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="56032-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56032-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56032-126">Next steps</span></span>

<span data-ttu-id="56032-127">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56032-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="56032-128">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="56032-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
