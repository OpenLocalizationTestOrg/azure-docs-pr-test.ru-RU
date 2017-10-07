---
title: "Пример сценария PowerShell - aaaAzure наблюдения за веб-приложения в журналы веб-сервера | Документы Microsoft"
description: "Пример сценария Azure PowerShell для мониторинга веб-приложения с помощью журналов веб-сервера."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="3d8c4-103">Мониторинг веб-приложения с помощью журналов веб-сервера</span><span class="sxs-lookup"><span data-stu-id="3d8c4-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="3d8c4-104">В этом случае будет создавать группы ресурсов, план обслуживания приложений, веб-приложения и настройте журналы hello web app tooenable веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="3d8c4-105">Затем вы загружаете hello файлы журналов для просмотра.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="3d8c4-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3d8c4-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3d8c4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3d8c4-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="3d8c4-108">Clean up deployment</span></span> 

<span data-ttu-id="3d8c4-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3d8c4-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3d8c4-110">Script explanation</span></span>

<span data-ttu-id="3d8c4-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-111">This script uses hello following commands.</span></span> <span data-ttu-id="3d8c4-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3d8c4-113">Команда</span><span class="sxs-lookup"><span data-stu-id="3d8c4-113">Command</span></span> | <span data-ttu-id="3d8c4-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="3d8c4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3d8c4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3d8c4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3d8c4-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3d8c4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3d8c4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3d8c4-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3d8c4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3d8c4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3d8c4-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="3d8c4-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3d8c4-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="3d8c4-122">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="3d8c4-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="3d8c4-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="3d8c4-124">Возвращает метрики веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="3d8c4-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d8c4-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d8c4-125">Next steps</span></span>

<span data-ttu-id="3d8c4-126">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3d8c4-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3d8c4-127">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3d8c4-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
