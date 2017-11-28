---
title: "Пример сценария PowerShell - aaaAzure масштабировать веб-приложения вручную | Документы Microsoft"
description: "Пример сценария Azure PowerShell для масштабирования веб-приложения вручную."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="52ba0-103">Масштабирование веб-приложения вручную</span><span class="sxs-lookup"><span data-stu-id="52ba0-103">Scale a web app manually</span></span>

<span data-ttu-id="52ba0-104">В этом сценарии вы узнаете toocreate группу ресурсов, приложение службы плана и веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="52ba0-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="52ba0-105">Затем будет масштабироваться hello план служб приложений из toomultiple единственных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="52ba0-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="52ba0-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="52ba0-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="52ba0-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="52ba0-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="52ba0-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="52ba0-108">Clean up deployment</span></span> 

<span data-ttu-id="52ba0-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="52ba0-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="52ba0-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="52ba0-110">Script explanation</span></span>

<span data-ttu-id="52ba0-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="52ba0-111">This script uses hello following commands.</span></span> <span data-ttu-id="52ba0-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="52ba0-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="52ba0-113">Команда</span><span class="sxs-lookup"><span data-stu-id="52ba0-113">Command</span></span> | <span data-ttu-id="52ba0-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="52ba0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="52ba0-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="52ba0-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="52ba0-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="52ba0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="52ba0-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="52ba0-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="52ba0-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="52ba0-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="52ba0-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="52ba0-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="52ba0-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="52ba0-120">Creates a web app.</span></span> |
| [<span data-ttu-id="52ba0-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="52ba0-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="52ba0-122">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="52ba0-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52ba0-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="52ba0-123">Next steps</span></span>

<span data-ttu-id="52ba0-124">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52ba0-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="52ba0-125">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="52ba0-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
