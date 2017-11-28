---
title: "Пример сценария PowerShell - aaaAzure Создание веб-приложения с непрерывным развертыванием из GitHub | Документы Microsoft"
description: "Пример сценария Azure PowerShell для создания веб-приложения с непрерывным развертыванием из GitHub."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="59b6b-103">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="59b6b-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="59b6b-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="59b6b-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="59b6b-105">Дополнительные сведения о развертывании GitHub без непрерывного развертывания см. в статье [Создание веб-приложения и развертывание кода из GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="59b6b-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="59b6b-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59b6b-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="59b6b-107">Кроме того, убедитесь в следующем.</span><span class="sxs-lookup"><span data-stu-id="59b6b-107">Also, ensure that:</span></span>

- <span data-ttu-id="59b6b-108">Соединение с Azure был создан с помощью hello `az login` команды.</span><span class="sxs-lookup"><span data-stu-id="59b6b-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="59b6b-109">код приложения Hello находится в открытые или закрытые репозитории GitHub, что вы являетесь владельцем.</span><span class="sxs-lookup"><span data-stu-id="59b6b-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="59b6b-110">Вы [создали маркер доступа в учетной записи GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="59b6b-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="59b6b-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="59b6b-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="59b6b-112">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="59b6b-112">Clean up deployment</span></span> 

<span data-ttu-id="59b6b-113">После выполнения сценария образец hello hello, следующая команда может быть группа ресурсов используется tooremove hello, веб-приложения и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="59b6b-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="59b6b-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="59b6b-114">Script explanation</span></span>

<span data-ttu-id="59b6b-115">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="59b6b-115">This script uses hello following commands.</span></span> <span data-ttu-id="59b6b-116">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="59b6b-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="59b6b-117">Команда</span><span class="sxs-lookup"><span data-stu-id="59b6b-117">Command</span></span> | <span data-ttu-id="59b6b-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="59b6b-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="59b6b-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="59b6b-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="59b6b-120">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="59b6b-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="59b6b-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="59b6b-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="59b6b-122">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="59b6b-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="59b6b-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="59b6b-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="59b6b-124">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="59b6b-124">Creates a web app.</span></span> |
| [<span data-ttu-id="59b6b-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="59b6b-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="59b6b-126">Изменяет ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="59b6b-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="59b6b-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59b6b-127">Next steps</span></span>

<span data-ttu-id="59b6b-128">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59b6b-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="59b6b-129">Дополнительные примеры Azure Powershell для веб-приложениях службы приложений Azure можно найти в hello [примеры Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="59b6b-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
