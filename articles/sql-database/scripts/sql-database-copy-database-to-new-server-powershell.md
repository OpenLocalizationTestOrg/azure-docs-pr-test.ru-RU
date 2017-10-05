---
title: "Пример для PowerShell. Копирование базы данных SQL Azure на новый сервер | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для копирования базы данных SQL на новый сервер"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="389d9-103">Копирование базы данных SQL на новый сервер с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="389d9-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="389d9-104">Этот пример сценария PowerShell создает копию существующей базы данных на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="389d9-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="389d9-105">Копирование базы данных на новый сервер</span><span class="sxs-lookup"><span data-stu-id="389d9-105">Copy a database to a new server</span></span>

<span data-ttu-id="389d9-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Копирование базы данных на новый сервер")]</span><span class="sxs-lookup"><span data-stu-id="389d9-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="389d9-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="389d9-107">Clean up deployment</span></span>

<span data-ttu-id="389d9-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="389d9-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="389d9-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="389d9-109">Script explanation</span></span>

<span data-ttu-id="389d9-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="389d9-110">This script uses the following commands.</span></span> <span data-ttu-id="389d9-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="389d9-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="389d9-112">Команда</span><span class="sxs-lookup"><span data-stu-id="389d9-112">Command</span></span> | <span data-ttu-id="389d9-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="389d9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="389d9-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="389d9-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="389d9-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="389d9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="389d9-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="389d9-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="389d9-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="389d9-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="389d9-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="389d9-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="389d9-119">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="389d9-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="389d9-120">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="389d9-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="389d9-121">Создает копию базы данных с помощью моментального снимка на текущий момент времени.</span><span class="sxs-lookup"><span data-stu-id="389d9-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="389d9-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="389d9-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="389d9-123">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="389d9-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="389d9-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="389d9-124">Next steps</span></span>

<span data-ttu-id="389d9-125">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="389d9-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="389d9-126">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="389d9-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
