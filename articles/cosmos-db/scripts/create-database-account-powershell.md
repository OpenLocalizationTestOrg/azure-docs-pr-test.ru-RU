---
title: "Создание учетной записи API DocumentDB для Azure Cosmos DB с помощью сценария Azure PowerShell | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания учетной записи API DocumentDB для Azure Cosmos DB."
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
ms.openlocfilehash: 9b54236ce3446fe1c6a2a30b31f6d91ad43a92d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="86515-103">Azure Cosmos DB: создание учетной записи API DocumentDB с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="86515-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="86515-104">Этот пример сценария PowerShell создает учетную запись API для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86515-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="86515-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="86515-105">Sample script</span></span>

<span data-ttu-id="86515-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Создание учетной записи для Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="86515-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="86515-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="86515-107">Clean up deployment</span></span>

<span data-ttu-id="86515-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="86515-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="86515-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="86515-109">Script explanation</span></span>

<span data-ttu-id="86515-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="86515-110">This script uses the following commands.</span></span> <span data-ttu-id="86515-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="86515-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="86515-112">Команда</span><span class="sxs-lookup"><span data-stu-id="86515-112">Command</span></span> | <span data-ttu-id="86515-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="86515-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="86515-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86515-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="86515-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="86515-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="86515-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="86515-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="86515-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="86515-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="86515-118">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="86515-118">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="86515-119">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="86515-119">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="86515-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="86515-120">Next steps</span></span>

<span data-ttu-id="86515-121">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="86515-121">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="86515-122">Дополнительные примеры скриптов PowerShell для базы данных Azure Cosmos DB можно найти [здесь](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="86515-122">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>