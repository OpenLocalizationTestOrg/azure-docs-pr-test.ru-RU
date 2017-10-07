---
title: "Пример сценария PowerShell - aaaAzure масштабировать веб-приложения по всему миру, архитектура высокого уровня доступности | Документы Microsoft"
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
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="483a2-103">Глобальное масштабирование веб-приложения с помощью высокодоступной архитектуры</span><span class="sxs-lookup"><span data-stu-id="483a2-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="483a2-104">В этом сценарии вы создадите группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="483a2-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="483a2-105">После завершения hello упражнении будет высокой, доступных архитектуру, позволяющую предоставляет общедоступный веб-приложения на основе минимальной задержки сети hello.</span><span class="sxs-lookup"><span data-stu-id="483a2-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="483a2-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="483a2-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="483a2-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="483a2-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="483a2-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="483a2-108">Clean up deployment</span></span> 

<span data-ttu-id="483a2-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="483a2-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="483a2-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="483a2-110">Script explanation</span></span>

<span data-ttu-id="483a2-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="483a2-111">This script uses hello following commands.</span></span> <span data-ttu-id="483a2-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="483a2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="483a2-113">Команда</span><span class="sxs-lookup"><span data-stu-id="483a2-113">Command</span></span> | <span data-ttu-id="483a2-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="483a2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="483a2-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="483a2-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="483a2-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="483a2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="483a2-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="483a2-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="483a2-118">Создает профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="483a2-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="483a2-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="483a2-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="483a2-120">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="483a2-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="483a2-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="483a2-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="483a2-122">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="483a2-122">Creates a web app.</span></span> |
| [<span data-ttu-id="483a2-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="483a2-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="483a2-124">Создает конечную точку в профиле диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="483a2-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="483a2-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="483a2-125">Next steps</span></span>

<span data-ttu-id="483a2-126">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="483a2-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="483a2-127">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="483a2-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
