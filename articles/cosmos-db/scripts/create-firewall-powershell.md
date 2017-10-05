---
title: "Создание брандмауэра для Azure Cosmos DB с помощью сценария Azure PowerShell | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания брандмауэра для Azure Cosmos DB."
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="d496c-103">Azure Cosmos DB: создание брандмауэра с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d496c-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="d496c-104">Этот пример сценария PowerShell создает брандмауэр для любой учетной записи API в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d496c-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d496c-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d496c-105">Sample script</span></span>

<span data-ttu-id="d496c-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Создание брандмауэра для Azure Cosmos DB")]</span><span class="sxs-lookup"><span data-stu-id="d496c-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d496c-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d496c-107">Clean up deployment</span></span>

<span data-ttu-id="d496c-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d496c-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d496c-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d496c-109">Script explanation</span></span>

<span data-ttu-id="d496c-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d496c-110">This script uses the following commands.</span></span> <span data-ttu-id="d496c-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d496c-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d496c-112">Команда</span><span class="sxs-lookup"><span data-stu-id="d496c-112">Command</span></span> | <span data-ttu-id="d496c-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="d496c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d496c-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d496c-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="d496c-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d496c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d496c-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d496c-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="d496c-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="d496c-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d496c-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="d496c-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="d496c-119">Изменяет учетную запись базы данных.</span><span class="sxs-lookup"><span data-stu-id="d496c-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="d496c-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d496c-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="d496c-121">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d496c-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d496c-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d496c-122">Next steps</span></span>

<span data-ttu-id="d496c-123">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="d496c-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="d496c-124">Дополнительные примеры скриптов PowerShell для базы данных Azure Cosmos DB можно найти [здесь](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d496c-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>