---
title: "Пример сценария PowerShell - маршрутизацию трафика для обеспечения высокой доступности приложений aaaAzure | Документы Microsoft"
description: "Пример скрипта Azure PowerShell для маршрутизация трафика с целью обеспечения высокой доступности приложений."
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="9d09d-103">Маршрутизация трафика для обеспечения высокой доступности приложений</span><span class="sxs-lookup"><span data-stu-id="9d09d-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="9d09d-104">Этот скрипт создает группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="9d09d-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="9d09d-105">Диспетчер трафика направляет трафик toohello приложения в одной области, как основной регион hello и дополнительный регион toohello при недоступности приложения hello в основном регионе hello.</span><span class="sxs-lookup"><span data-stu-id="9d09d-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="9d09d-106">Перед выполнением сценария hello, необходимо изменить hello MyWebApp, MyWebAppL1 и MyWebAppL2 значения toounique значения в пределах Azure.</span><span class="sxs-lookup"><span data-stu-id="9d09d-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="9d09d-107">После выполнения сценария hello, можно открыть приложение hello в основной регион hello с mywebapp.trafficmanager.net hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9d09d-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="9d09d-108">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="9d09d-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9d09d-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9d09d-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="9d09d-110">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="9d09d-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="9d09d-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="9d09d-111">Script explanation</span></span>

<span data-ttu-id="9d09d-112">Этот скрипт использует следующие команды toocreate группы ресурсов, веб-приложения, профиль диспетчера трафика hello и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9d09d-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="9d09d-113">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="9d09d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9d09d-114">Команда</span><span class="sxs-lookup"><span data-stu-id="9d09d-114">Command</span></span> | <span data-ttu-id="9d09d-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="9d09d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d09d-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9d09d-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="9d09d-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9d09d-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9d09d-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="9d09d-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="9d09d-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9d09d-119">Creates an App Service plan.</span></span> <span data-ttu-id="9d09d-120">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="9d09d-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9d09d-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="9d09d-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="9d09d-122">Создает веб-приложение Azure в течение hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="9d09d-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="9d09d-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9d09d-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="9d09d-124">Создает веб-приложение Azure в течение hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="9d09d-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="9d09d-125">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="9d09d-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="9d09d-126">Создает профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="9d09d-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="9d09d-127">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="9d09d-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="9d09d-128">Добавляет конечную точку tooan профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="9d09d-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d09d-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d09d-129">Next steps</span></span>

<span data-ttu-id="9d09d-130">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d09d-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="9d09d-131">Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d09d-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
