---
title: "Образец скрипта PowerShell - aaaAzure Создание веб-приложения и развертывания кода из локального репозитория Git | Документы Microsoft"
description: "Пример сценария Azure PowerShell для создания веб-приложения и развертывания кода из локального репозитория Git."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="fa6e4-103">Создание веб-приложения и развертывание кода из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="fa6e4-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="fa6e4-104">Этот пример скрипта создает веб-приложение со связанными ресурсами в службе приложений, а затем развертывает код веб-приложения в локальном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="fa6e4-105">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="fa6e4-106">Кроме того код приложения должен toobe, зафиксированных в локальном репозитории.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="fa6e4-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fa6e4-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fa6e4-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="fa6e4-108">Clean up deployment</span></span> 

<span data-ttu-id="fa6e4-109">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="fa6e4-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fa6e4-110">Script explanation</span></span>

<span data-ttu-id="fa6e4-111">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-111">This script uses hello following commands.</span></span> <span data-ttu-id="fa6e4-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fa6e4-113">Команда</span><span class="sxs-lookup"><span data-stu-id="fa6e4-113">Command</span></span> | <span data-ttu-id="fa6e4-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="fa6e4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fa6e4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fa6e4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fa6e4-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fa6e4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="fa6e4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="fa6e4-118">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="fa6e4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="fa6e4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="fa6e4-120">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="fa6e4-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="fa6e4-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="fa6e4-122">Изменяет ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="fa6e4-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="fa6e4-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="fa6e4-124">Получает профиль публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="fa6e4-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fa6e4-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa6e4-125">Next steps</span></span>

<span data-ttu-id="fa6e4-126">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fa6e4-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fa6e4-127">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fa6e4-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
