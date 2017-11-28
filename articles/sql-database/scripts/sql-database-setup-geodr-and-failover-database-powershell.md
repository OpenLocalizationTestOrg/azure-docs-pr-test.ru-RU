---
title: "aaaPowerShell пример active geo репликации одной базы данных SQL Azure | Документы Microsoft"
description: "Azure PowerShell пример сценария tooset копирование активную георепликацию для одной базы данных Azure SQL"
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
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="8fd81-103">Используйте PowerShell tooconfigure активную георепликацию для одной базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="8fd81-103">Use PowerShell tooconfigure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="8fd81-104">В этом примере сценария PowerShell настраивает активную георепликацию для одной базы данных Azure SQL и отказа tooa вторичной реплики базы данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="8fd81-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="8fd81-105">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="8fd81-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8fd81-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="8fd81-106">Clean up deployment</span></span>

<span data-ttu-id="8fd81-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="8fd81-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="8fd81-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="8fd81-108">Script explanation</span></span>

<span data-ttu-id="8fd81-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="8fd81-109">This script uses hello following commands.</span></span> <span data-ttu-id="8fd81-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="8fd81-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8fd81-111">Команда</span><span class="sxs-lookup"><span data-stu-id="8fd81-111">Command</span></span> | <span data-ttu-id="8fd81-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="8fd81-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8fd81-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8fd81-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8fd81-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8fd81-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8fd81-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="8fd81-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="8fd81-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="8fd81-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="8fd81-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="8fd81-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="8fd81-118">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="8fd81-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="8fd81-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8fd81-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="8fd81-120">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="8fd81-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="8fd81-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8fd81-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="8fd81-122">Создает базу данных-получатель для существующей базы данных и начинает репликацию данных.</span><span class="sxs-lookup"><span data-stu-id="8fd81-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="8fd81-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="8fd81-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="8fd81-124">Получает одну или несколько баз данных.</span><span class="sxs-lookup"><span data-stu-id="8fd81-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="8fd81-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8fd81-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="8fd81-126">Переключает основной tooinitiate toobe отработки отказа базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="8fd81-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="8fd81-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="8fd81-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="8fd81-128">Получает ссылки hello географическую репликацию данных между базы данных SQL Azure и группы ресурсов или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8fd81-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="8fd81-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="8fd81-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="8fd81-130">Завершает репликацию данных между базой данных SQL и hello указанной базы данных-получателя.</span><span class="sxs-lookup"><span data-stu-id="8fd81-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="8fd81-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8fd81-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8fd81-132">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="8fd81-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="8fd81-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fd81-133">Next steps</span></span>

<span data-ttu-id="8fd81-134">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8fd81-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8fd81-135">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8fd81-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
