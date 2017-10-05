---
title: "Пример сценария Azure PowerShell. Создание веб-приложения с непрерывным развертыванием из GitHub | Документация Майкрософт"
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
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="5185e-103">Создание веб-приложения с непрерывным развертыванием из GitHub</span><span class="sxs-lookup"><span data-stu-id="5185e-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="5185e-104">Этот пример скрипта создает веб-приложение в службе приложений со связанными ресурсами, а затем настраивает непрерывное развертывание из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="5185e-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="5185e-105">Дополнительные сведения о развертывании GitHub без непрерывного развертывания см. в статье [Создание веб-приложения и развертывание кода из GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="5185e-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="5185e-106">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5185e-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="5185e-107">Кроме того, убедитесь в следующем.</span><span class="sxs-lookup"><span data-stu-id="5185e-107">Also, ensure that:</span></span>

- <span data-ttu-id="5185e-108">Подключение к Azure установлено с помощью команды `az login`.</span><span class="sxs-lookup"><span data-stu-id="5185e-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="5185e-109">Код приложения находится в вашем открытом или закрытом репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="5185e-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="5185e-110">Вы [создали маркер доступа в учетной записи GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="5185e-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="5185e-111">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5185e-111">Sample script</span></span>

<span data-ttu-id="5185e-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Создание веб-приложения с непрерывным развертыванием из GitHub")]</span><span class="sxs-lookup"><span data-stu-id="5185e-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5185e-113">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="5185e-113">Clean up deployment</span></span> 

<span data-ttu-id="5185e-114">Выполнив пример сценария, вы можете удалить группу ресурсов, веб-приложение и все связанные ресурсы, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="5185e-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="5185e-115">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5185e-115">Script explanation</span></span>

<span data-ttu-id="5185e-116">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="5185e-116">This script uses the following commands.</span></span> <span data-ttu-id="5185e-117">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5185e-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5185e-118">Команда</span><span class="sxs-lookup"><span data-stu-id="5185e-118">Command</span></span> | <span data-ttu-id="5185e-119">Примечания</span><span class="sxs-lookup"><span data-stu-id="5185e-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5185e-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5185e-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5185e-121">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5185e-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5185e-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="5185e-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="5185e-123">Создает план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5185e-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="5185e-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="5185e-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="5185e-125">Создает веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="5185e-125">Creates a web app.</span></span> |
| [<span data-ttu-id="5185e-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5185e-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="5185e-127">Изменяет ресурс в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5185e-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5185e-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5185e-128">Next steps</span></span>

<span data-ttu-id="5185e-129">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5185e-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5185e-130">Дополнительные примеры сценариев Azure PowerShell для веб-приложений службы приложений Azure доступны [здесь](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5185e-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
