---
title: "Пример сценария Azure PowerShell. Создание веб-приложения и развертывание кода в промежуточной среде | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания веб-приложения и развертывания кода в промежуточной среде."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 55adc13350eb0f4711efa3c901f6e4e7755dfb27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="73fac-103">Создание веб-приложения и развертывание кода в промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="73fac-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="73fac-104">Этот пример скрипта создает веб-приложение в службе приложений с дополнительным слотом развертывания под названием staging, а затем развертывает в нем пример приложения.</span><span class="sxs-lookup"><span data-stu-id="73fac-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

<span data-ttu-id="73fac-105">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="73fac-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="73fac-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="73fac-106">Sample script</span></span>

<span data-ttu-id="73fac-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Создание веб-приложения и развертывание кода в промежуточной среде")]</span><span class="sxs-lookup"><span data-stu-id="73fac-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code to a staging environment")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="73fac-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="73fac-108">Clean up deployment</span></span> 

<span data-ttu-id="73fac-109">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="73fac-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="73fac-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="73fac-110">Script explanation</span></span>

<span data-ttu-id="73fac-111">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="73fac-111">This script uses the following commands.</span></span> <span data-ttu-id="73fac-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="73fac-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="73fac-113">Команда</span><span class="sxs-lookup"><span data-stu-id="73fac-113">Command</span></span> | <span data-ttu-id="73fac-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="73fac-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="73fac-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="73fac-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="73fac-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="73fac-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="73fac-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="73fac-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="73fac-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="73fac-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="73fac-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="73fac-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="73fac-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="73fac-120">Creates a web app.</span></span> |
| [<span data-ttu-id="73fac-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="73fac-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="73fac-122">Обновляет план службы приложений для изменения ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="73fac-122">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="73fac-123">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="73fac-123">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="73fac-124">Создает слот развертывания для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="73fac-124">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="73fac-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="73fac-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="73fac-126">Изменяет ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="73fac-126">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="73fac-127">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="73fac-127">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="73fac-128">Переключает слот развертывания веб-приложения на рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="73fac-128">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="73fac-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73fac-129">Next steps</span></span>

<span data-ttu-id="73fac-130">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="73fac-130">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="73fac-131">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="73fac-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
