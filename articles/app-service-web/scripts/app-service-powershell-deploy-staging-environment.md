---
title: "aaaAzure образец скрипта PowerShell - создания веб-приложения и развертывания кода tooa промежуточной среде | Документы Microsoft"
description: "Azure образец скрипта PowerShell - создания веб-приложения и развертывания кода tooa промежуточной среде"
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
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="3b416-103">Создание веб-приложения и развертывание кода tooa промежуточной среде</span><span class="sxs-lookup"><span data-stu-id="3b416-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="3b416-104">Этот образец скрипта создает веб-приложения в службе приложений слотом развертывания называется «промежуточный», а затем развернет toohello образец приложения, «промежуточный» слоте.</span><span class="sxs-lookup"><span data-stu-id="3b416-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="3b416-105">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="3b416-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3b416-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3b416-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3b416-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="3b416-107">Clean up deployment</span></span> 

<span data-ttu-id="3b416-108">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3b416-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3b416-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3b416-109">Script explanation</span></span>

<span data-ttu-id="3b416-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="3b416-110">This script uses hello following commands.</span></span> <span data-ttu-id="3b416-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="3b416-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3b416-112">Команда</span><span class="sxs-lookup"><span data-stu-id="3b416-112">Command</span></span> | <span data-ttu-id="3b416-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="3b416-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3b416-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b416-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3b416-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3b416-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3b416-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3b416-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3b416-117">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="3b416-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3b416-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3b416-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3b416-119">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="3b416-119">Creates a web app.</span></span> |
| [<span data-ttu-id="3b416-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3b416-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="3b416-121">Изменяет его цен toochange плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="3b416-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="3b416-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="3b416-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="3b416-123">Создает слот развертывания для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3b416-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="3b416-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="3b416-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="3b416-125">Изменяет ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3b416-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="3b416-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="3b416-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="3b416-127">Переключает слот развертывания веб-приложения на рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="3b416-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3b416-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b416-128">Next steps</span></span>

<span data-ttu-id="3b416-129">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3b416-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3b416-130">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3b416-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
