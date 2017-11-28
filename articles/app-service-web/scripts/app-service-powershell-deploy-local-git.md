---
title: "Пример сценария Azure PowerShell. Создание веб-приложения и развертывание кода из локального репозитория Git | Документация Майкрософт"
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
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="6e4d9-103">Создание веб-приложения и развертывание кода из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="6e4d9-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="6e4d9-104">Этот пример скрипта создает веб-приложение со связанными ресурсами в службе приложений, а затем развертывает код веб-приложения в локальном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="6e4d9-105">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](/powershell/azure/overview), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="6e4d9-106">Кроме того, код приложения нужно зафиксировать в локальном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6e4d9-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6e4d9-107">Sample script</span></span>

<span data-ttu-id="6e4d9-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Создание веб-приложения и развертывание кода из локального репозитория Git")]</span><span class="sxs-lookup"><span data-stu-id="6e4d9-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6e4d9-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="6e4d9-109">Clean up deployment</span></span> 

<span data-ttu-id="6e4d9-110">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6e4d9-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6e4d9-111">Script explanation</span></span>

<span data-ttu-id="6e4d9-112">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-112">This script uses the following commands.</span></span> <span data-ttu-id="6e4d9-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6e4d9-114">Команда</span><span class="sxs-lookup"><span data-stu-id="6e4d9-114">Command</span></span> | <span data-ttu-id="6e4d9-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="6e4d9-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6e4d9-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e4d9-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6e4d9-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6e4d9-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6e4d9-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6e4d9-119">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6e4d9-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6e4d9-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6e4d9-121">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-121">Creates a web app.</span></span> |
| [<span data-ttu-id="6e4d9-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="6e4d9-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="6e4d9-123">Изменяет ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="6e4d9-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="6e4d9-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="6e4d9-125">Получает профиль публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6e4d9-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6e4d9-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e4d9-126">Next steps</span></span>

<span data-ttu-id="6e4d9-127">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e4d9-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6e4d9-128">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6e4d9-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
