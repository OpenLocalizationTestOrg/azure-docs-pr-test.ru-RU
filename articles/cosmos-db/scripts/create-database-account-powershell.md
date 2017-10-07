---
title: "PowerShell скрипта создайте учетную запись Azure Cosmos DB DocumentDB API aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: f0751faeca3c1de5906b675e736c58f3d5beaea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="7fa24-103">Azure Cosmos DB: создание учетной записи API DocumentDB с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fa24-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="7fa24-104">Этот пример сценария PowerShell создает учетную запись API для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7fa24-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="7fa24-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="7fa24-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7fa24-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="7fa24-106">Clean up deployment</span></span>

<span data-ttu-id="7fa24-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="7fa24-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7fa24-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="7fa24-108">Script explanation</span></span>

<span data-ttu-id="7fa24-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="7fa24-109">This script uses hello following commands.</span></span> <span data-ttu-id="7fa24-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="7fa24-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7fa24-111">Команда</span><span class="sxs-lookup"><span data-stu-id="7fa24-111">Command</span></span> | <span data-ttu-id="7fa24-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="7fa24-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7fa24-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7fa24-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="7fa24-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7fa24-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7fa24-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="7fa24-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="7fa24-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="7fa24-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="7fa24-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7fa24-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="7fa24-118">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="7fa24-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="7fa24-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fa24-119">Next steps</span></span>

<span data-ttu-id="7fa24-120">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="7fa24-120">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="7fa24-121">Дополнительные примеры сценариев, использующих DB Cosmos Azure PowerShell можно найти в hello [скриптов Azure Cosmos DB PowerShell](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7fa24-121">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
