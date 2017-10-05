---
title: "Создание политики отработки отказа для базы данных Azure Cosmos DB с помощью скрипта Azure PowerShell | Документация Майкрософт"
description: "Пример скрипта Azure PowerShell. Создание политики отработки отказа для базы данных Azure Cosmos DB"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 16da3cd543ccbb7fe346261f91d2e9a3ceaf3a8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-failover-policy-for-high-availability-using-powershell"></a><span data-ttu-id="9a18f-103">Создание политики отработки отказа базы данных Azure Cosmos DB для обеспечения высокой доступности с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a18f-103">Create an Azure Cosmos DB failover policy for high availability using PowerShell</span></span>

<span data-ttu-id="9a18f-104">Этот пример скрипта PowerShell создает политику отработки отказа для обеспечения высокой доступности базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9a18f-104">This sample PowerShell script creates a failover policy for high availability for Azure Cosmos DB.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9a18f-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9a18f-105">Sample script</span></span>

<span data-ttu-id="9a18f-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Создание учетной записи API DocumentDB для базы данных Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="9a18f-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Create an Azure Cosmos DB DocumentDB API account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9a18f-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="9a18f-107">Clean up deployment</span></span>

<span data-ttu-id="9a18f-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="9a18f-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9a18f-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="9a18f-109">Script explanation</span></span>

<span data-ttu-id="9a18f-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="9a18f-110">This script uses the following commands.</span></span> <span data-ttu-id="9a18f-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="9a18f-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9a18f-112">Команда</span><span class="sxs-lookup"><span data-stu-id="9a18f-112">Command</span></span> | <span data-ttu-id="9a18f-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="9a18f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9a18f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a18f-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="9a18f-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9a18f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9a18f-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9a18f-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="9a18f-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="9a18f-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="9a18f-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="9a18f-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="9a18f-119">Вызывает действие для учетной записи базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9a18f-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="9a18f-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9a18f-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="9a18f-121">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="9a18f-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="9a18f-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a18f-122">Next steps</span></span>

<span data-ttu-id="9a18f-123">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="9a18f-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="9a18f-124">Дополнительные примеры скриптов PowerShell для базы данных Azure Cosmos DB можно найти [здесь](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9a18f-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>