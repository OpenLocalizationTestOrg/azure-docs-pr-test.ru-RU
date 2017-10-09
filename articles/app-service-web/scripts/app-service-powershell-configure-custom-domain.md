---
title: "aaaAzure образец скрипта PowerShell - назначить веб-приложения tooa личного домена | Документы Microsoft"
description: "Azure образец скрипта PowerShell - Assign пользовательского домена tooa веб-приложения"
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
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="a2533-103">Назначить пользовательский домен tooa веб-приложения</span><span class="sxs-lookup"><span data-stu-id="a2533-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="a2533-104">Этот образец скрипта создает веб-приложения в службе приложений с его связанные ресурсы и затем отображает `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="a2533-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="a2533-105">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="a2533-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="a2533-106">Кроме того необходимо, чтобы страница конфигурации toohave доступа tooyour регистратора домена DNS.</span><span class="sxs-lookup"><span data-stu-id="a2533-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a2533-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="a2533-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a2533-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="a2533-108">Clean up deployment</span></span> 

<span data-ttu-id="a2533-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a2533-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a2533-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="a2533-110">Script explanation</span></span>

<span data-ttu-id="a2533-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="a2533-111">This script uses hello following commands.</span></span> <span data-ttu-id="a2533-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="a2533-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a2533-113">Команда</span><span class="sxs-lookup"><span data-stu-id="a2533-113">Command</span></span> | <span data-ttu-id="a2533-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="a2533-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2533-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2533-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a2533-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a2533-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2533-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a2533-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a2533-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="a2533-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a2533-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a2533-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a2533-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="a2533-120">Creates a web app.</span></span> |
| [<span data-ttu-id="a2533-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a2533-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="a2533-122">Изменяет его цен toochange плана служб приложений.</span><span class="sxs-lookup"><span data-stu-id="a2533-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="a2533-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a2533-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="a2533-124">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a2533-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a2533-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2533-125">Next steps</span></span>

<span data-ttu-id="a2533-126">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2533-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a2533-127">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2533-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
