---
title: "Пример скрипта Azure PowerShell. Назначение пользовательского домена веб-приложению | Документация Майкрософт"
description: "Пример скрипта Azure PowerShell. Назначение пользовательского домена веб-приложению"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="ccafd-103">Назначение пользовательского домена веб-приложению</span><span class="sxs-lookup"><span data-stu-id="ccafd-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="ccafd-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем сопоставляет с ним `www.<yourdomain>`.</span><span class="sxs-lookup"><span data-stu-id="ccafd-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="ccafd-105">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="ccafd-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="ccafd-106">Кроме того, нужен доступ к странице конфигурации DNS вашего регистратора доменных имен.</span><span class="sxs-lookup"><span data-stu-id="ccafd-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ccafd-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ccafd-107">Sample script</span></span>

<span data-ttu-id="ccafd-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Назначение пользовательского домена веб-приложению")]</span><span class="sxs-lookup"><span data-stu-id="ccafd-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ccafd-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ccafd-109">Clean up deployment</span></span> 

<span data-ttu-id="ccafd-110">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="ccafd-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="ccafd-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ccafd-111">Script explanation</span></span>

<span data-ttu-id="ccafd-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ccafd-112">This script uses the following commands.</span></span> <span data-ttu-id="ccafd-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="ccafd-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ccafd-114">Команда</span><span class="sxs-lookup"><span data-stu-id="ccafd-114">Command</span></span> | <span data-ttu-id="ccafd-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="ccafd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ccafd-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ccafd-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ccafd-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ccafd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ccafd-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ccafd-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="ccafd-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ccafd-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ccafd-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ccafd-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="ccafd-121">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="ccafd-121">Creates a web app.</span></span> |
| [<span data-ttu-id="ccafd-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ccafd-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="ccafd-123">Обновляет план службы приложений для изменения ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="ccafd-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="ccafd-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ccafd-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="ccafd-125">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ccafd-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ccafd-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ccafd-126">Next steps</span></span>

<span data-ttu-id="ccafd-127">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ccafd-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ccafd-128">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ccafd-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
