---
title: "База данных SQL aaaPowerShell пример restore-резервного копирования Azure | Документы Microsoft"
description: "Azure PowerShell пример сценария toorestore базу данных Azure SQL из географически избыточная резервных копий"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="fd653-103">Используйте PowerShell toorestore базу данных Azure SQL из резервных копий</span><span class="sxs-lookup"><span data-stu-id="fd653-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="fd653-104">В этом примере сценария PowerShell восстанавливает базу данных Azure SQL из геоизбыточной резервной копии, восстановление удаленных Azure SQL базы данных tooits последней резервной копии и производится восстановление базы данных Azure SQL tooa определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="fd653-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="fd653-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fd653-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fd653-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="fd653-106">Clean up deployment</span></span>

<span data-ttu-id="fd653-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="fd653-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fd653-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fd653-108">Script explanation</span></span>

<span data-ttu-id="fd653-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="fd653-109">This script uses hello following commands.</span></span> <span data-ttu-id="fd653-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="fd653-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fd653-111">Команда</span><span class="sxs-lookup"><span data-stu-id="fd653-111">Command</span></span> | <span data-ttu-id="fd653-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="fd653-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd653-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd653-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="fd653-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fd653-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="fd653-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="fd653-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fd653-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="fd653-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="fd653-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fd653-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="fd653-118">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="fd653-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="fd653-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="fd653-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="fd653-120">Получает геоизбыточную резервную копию базы данных.</span><span class="sxs-lookup"><span data-stu-id="fd653-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="fd653-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fd653-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="fd653-122">Восстанавливает базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fd653-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="fd653-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fd653-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="fd653-124">Удаляет базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fd653-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="fd653-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="fd653-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="fd653-126">Получает удаленную базу данных, которую можно восстановить.</span><span class="sxs-lookup"><span data-stu-id="fd653-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="fd653-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd653-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fd653-128">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="fd653-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd653-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd653-129">Next steps</span></span>

<span data-ttu-id="fd653-130">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd653-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fd653-131">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fd653-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
