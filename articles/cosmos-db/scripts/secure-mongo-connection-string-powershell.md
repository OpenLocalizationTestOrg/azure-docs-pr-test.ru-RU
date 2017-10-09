---
title: "aaaAzure строка подключения DB Cosmos Azure Get сценария PowerShell для приложений MongoDB | Документы Microsoft"
description: "Пример скрипта Azure PowerShell. Получение строки подключения базы данных Azure Cosmos DB для приложений MongoDB"
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
ms.openlocfilehash: d04502b8f59bb6f3cb8bec696595f962b479fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="33b16-103">Получение строки подключения базы данных Azure Cosmos DB для приложений MongoDB с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="33b16-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="33b16-104">Этот пример получает строку подключения базы данных Azure Cosmos DB для приложений MongoDB с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33b16-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="33b16-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="33b16-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get hello MongoDB connection string from an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="33b16-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="33b16-106">Clean up deployment</span></span>

<span data-ttu-id="33b16-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="33b16-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="33b16-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="33b16-108">Script explanation</span></span>

<span data-ttu-id="33b16-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="33b16-109">This script uses hello following commands.</span></span> <span data-ttu-id="33b16-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="33b16-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="33b16-111">Команда</span><span class="sxs-lookup"><span data-stu-id="33b16-111">Command</span></span> | <span data-ttu-id="33b16-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="33b16-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="33b16-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="33b16-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="33b16-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="33b16-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="33b16-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="33b16-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="33b16-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="33b16-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="33b16-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="33b16-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="33b16-118">Вызывает действие для учетной записи Azure CosmosDB hello.</span><span class="sxs-lookup"><span data-stu-id="33b16-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="33b16-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="33b16-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="33b16-120">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="33b16-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="33b16-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33b16-121">Next steps</span></span>

<span data-ttu-id="33b16-122">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="33b16-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="33b16-123">Дополнительные примеры сценариев, использующих DB Cosmos Azure PowerShell можно найти в hello [скриптов Azure Cosmos DB PowerShell](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="33b16-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
