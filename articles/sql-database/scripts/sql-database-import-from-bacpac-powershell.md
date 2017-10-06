---
title: "База данных SQL Azure файла примера импорта bacpac aaaPowerShell | Документы Microsoft"
description: "Azure PowerShell пример сценария tooimport bacpac плитки в базе данных SQL"
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="55cd7-103">Используйте PowerShell tooimport файл bacpac в базу данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="55cd7-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="55cd7-104">Этот пример сценария PowerShell импортирует базу данных из **BACPAC**-файла на в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="55cd7-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="55cd7-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="55cd7-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="55cd7-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="55cd7-106">Clean up deployment</span></span>

<span data-ttu-id="55cd7-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="55cd7-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="55cd7-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="55cd7-108">Script explanation</span></span>

<span data-ttu-id="55cd7-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="55cd7-109">This script uses hello following commands.</span></span> <span data-ttu-id="55cd7-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="55cd7-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="55cd7-111">Команда</span><span class="sxs-lookup"><span data-stu-id="55cd7-111">Command</span></span> | <span data-ttu-id="55cd7-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="55cd7-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55cd7-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="55cd7-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="55cd7-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="55cd7-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55cd7-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="55cd7-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="55cd7-116">Создает логический сервер, что узлы hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="55cd7-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="55cd7-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="55cd7-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="55cd7-118">Создает брандмауэра правило tooallow доступа tooall баз данных SQL на сервере hello из hello ввести диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="55cd7-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="55cd7-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="55cd7-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="55cd7-120">Импортирует a .bacpac файл и создать новую базу данных на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="55cd7-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="55cd7-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="55cd7-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="55cd7-122">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="55cd7-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55cd7-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55cd7-123">Next steps</span></span>

<span data-ttu-id="55cd7-124">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55cd7-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="55cd7-125">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="55cd7-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
