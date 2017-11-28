---
title: "Пример скрипта Azure PowerShell. Маршрутизация трафика для обеспечения высокой доступности приложений | Документация Майкрософт"
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
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="191ca-103">Маршрутизация трафика для обеспечения высокой доступности приложений</span><span class="sxs-lookup"><span data-stu-id="191ca-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="191ca-104">Этот скрипт создает группу ресурсов, два плана службы приложений, два веб-приложения, профиль и две конечные точки диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="191ca-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="191ca-105">Диспетчер трафика направляет трафик в приложение в основном регионе. Если оно недоступно, трафик направляется в дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="191ca-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="191ca-106">Перед выполнением этого скрипта необходимо задать уникальные в Azure значения MyWebApp, MyWebAppL1 и MyWebAppL2.</span><span class="sxs-lookup"><span data-stu-id="191ca-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="191ca-107">После выполнения вы сможете подключиться к приложению в основном регионе, используя URL-адрес mywebapp.trafficmanager.net.</span><span class="sxs-lookup"><span data-stu-id="191ca-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="191ca-108">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="191ca-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="191ca-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="191ca-109">Sample script</span></span>

<span data-ttu-id="191ca-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Маршрутизация трафика для обеспечения высокой доступности")]</span><span class="sxs-lookup"><span data-stu-id="191ca-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="191ca-111">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="191ca-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="191ca-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="191ca-112">Script explanation</span></span>

<span data-ttu-id="191ca-113">Для создания группы ресурсов, веб-приложения, профиля диспетчера трафика и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="191ca-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="191ca-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="191ca-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="191ca-115">Команда</span><span class="sxs-lookup"><span data-stu-id="191ca-115">Command</span></span> | <span data-ttu-id="191ca-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="191ca-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="191ca-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="191ca-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="191ca-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="191ca-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="191ca-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="191ca-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="191ca-120">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="191ca-120">Creates an App Service plan.</span></span> <span data-ttu-id="191ca-121">Это как ферма сервера для веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="191ca-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="191ca-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="191ca-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="191ca-123">Создает веб-приложение Azure в плане службы приложений.</span><span class="sxs-lookup"><span data-stu-id="191ca-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="191ca-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="191ca-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="191ca-125">Создает веб-приложение Azure в плане службы приложений.</span><span class="sxs-lookup"><span data-stu-id="191ca-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="191ca-126">New-AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="191ca-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="191ca-127">Создает профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="191ca-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="191ca-128">New-AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="191ca-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="191ca-129">Добавляет конечную точку в профиль диспетчера трафика Azure.</span><span class="sxs-lookup"><span data-stu-id="191ca-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="191ca-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="191ca-130">Next steps</span></span>

<span data-ttu-id="191ca-131">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="191ca-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="191ca-132">Дополнительные примеры скриптов PowerShell для сетей см. в [обзорной документации по сетям Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="191ca-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>