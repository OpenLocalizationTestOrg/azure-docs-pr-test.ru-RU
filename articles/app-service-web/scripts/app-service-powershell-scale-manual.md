---
title: "Пример сценария Azure PowerShell. Масштабирование веб-приложения вручную | Документация Майкрософт"
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
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="575e7-103">Масштабирование веб-приложения вручную</span><span class="sxs-lookup"><span data-stu-id="575e7-103">Scale a web app manually</span></span>

<span data-ttu-id="575e7-104">В этой статье вы узнаете, как создать группу ресурсов, план службы приложений и веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="575e7-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="575e7-105">Затем вы выполните масштабирование плана службы приложений от одного экземпляра до нескольких.</span><span class="sxs-lookup"><span data-stu-id="575e7-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="575e7-106">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="575e7-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="575e7-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="575e7-107">Sample script</span></span>

<span data-ttu-id="575e7-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Масштабирование веб-приложения вручную")]</span><span class="sxs-lookup"><span data-stu-id="575e7-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="575e7-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="575e7-109">Clean up deployment</span></span> 

<span data-ttu-id="575e7-110">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="575e7-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="575e7-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="575e7-111">Script explanation</span></span>

<span data-ttu-id="575e7-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="575e7-112">This script uses the following commands.</span></span> <span data-ttu-id="575e7-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="575e7-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="575e7-114">Команда</span><span class="sxs-lookup"><span data-stu-id="575e7-114">Command</span></span> | <span data-ttu-id="575e7-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="575e7-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="575e7-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="575e7-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="575e7-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="575e7-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="575e7-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="575e7-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="575e7-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="575e7-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="575e7-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="575e7-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="575e7-121">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="575e7-121">Creates a web app.</span></span> |
| [<span data-ttu-id="575e7-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="575e7-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="575e7-123">Изменяет конфигурацию веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="575e7-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="575e7-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="575e7-124">Next steps</span></span>

<span data-ttu-id="575e7-125">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="575e7-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="575e7-126">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="575e7-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
