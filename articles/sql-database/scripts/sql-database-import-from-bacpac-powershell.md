---
title: "Пример для PowerShell. Импорт BACPAC-файла в базу данных SQL Azure | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для импорта BACPAC-файла в базу данных SQL."
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
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="7ce9b-103">Импорт BACPAC-файла в базу данных SQL Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ce9b-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="7ce9b-104">Этот пример сценария PowerShell импортирует базу данных из **BACPAC**-файла на в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="7ce9b-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="7ce9b-105">Sample script</span></span>

<span data-ttu-id="7ce9b-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Создание базы данных SQL")]</span><span class="sxs-lookup"><span data-stu-id="7ce9b-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7ce9b-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="7ce9b-107">Clean up deployment</span></span>

<span data-ttu-id="7ce9b-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7ce9b-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="7ce9b-109">Script explanation</span></span>

<span data-ttu-id="7ce9b-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-110">This script uses the following commands.</span></span> <span data-ttu-id="7ce9b-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7ce9b-112">Команда</span><span class="sxs-lookup"><span data-stu-id="7ce9b-112">Command</span></span> | <span data-ttu-id="7ce9b-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="7ce9b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7ce9b-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7ce9b-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7ce9b-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7ce9b-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="7ce9b-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7ce9b-117">Создает логический сервер, на котором размещена база данных SQL.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="7ce9b-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="7ce9b-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="7ce9b-119">Создает правило брандмауэра, чтобы разрешить доступ ко всем базам данных SQL на сервере по введенному диапазону IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="7ce9b-120">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="7ce9b-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="7ce9b-121">Импортирует BACPAC-файл и создает из него базу данных на сервере.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="7ce9b-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7ce9b-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7ce9b-123">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="7ce9b-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7ce9b-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ce9b-124">Next steps</span></span>

<span data-ttu-id="7ce9b-125">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7ce9b-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7ce9b-126">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7ce9b-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
