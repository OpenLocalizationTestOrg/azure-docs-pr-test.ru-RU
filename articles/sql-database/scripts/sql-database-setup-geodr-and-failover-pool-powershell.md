---
title: "Пример для PowerShell. Активная георепликация базы данных SQL Azure в пуле | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для настройки активной георепликации базы данных SQL Azure в составе пула."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: c1a495a8f9960ed60d8589dee9615e075f80c77b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="ba2e4-103">Настройка активной георепликации для базы данных SQL Azure в составе пула с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba2e4-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="ba2e4-104">Этот пример сценария PowerShell настраивает активную георепликацию для базы данных SQL Azure в эластичном пуле и выполняет для нее отработку отказа во вторичную реплику базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="ba2e4-105">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="ba2e4-105">Sample scripts</span></span>

<span data-ttu-id="ba2e4-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Настройка активной георепликации для эластичного пула")]</span><span class="sxs-lookup"><span data-stu-id="ba2e4-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ba2e4-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ba2e4-107">Clean up deployment</span></span>

<span data-ttu-id="ba2e4-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="ba2e4-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ba2e4-109">Script explanation</span></span>

<span data-ttu-id="ba2e4-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-110">This script uses the following commands.</span></span> <span data-ttu-id="ba2e4-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ba2e4-112">Команда</span><span class="sxs-lookup"><span data-stu-id="ba2e4-112">Command</span></span> | <span data-ttu-id="ba2e4-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="ba2e4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba2e4-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ba2e4-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ba2e4-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba2e4-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="ba2e4-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="ba2e4-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="ba2e4-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="ba2e4-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="ba2e4-119">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="ba2e4-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ba2e4-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="ba2e4-121">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="ba2e4-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ba2e4-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="ba2e4-123">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="ba2e4-124">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="ba2e4-124">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="ba2e4-125">Создает базу данных-получатель для существующей базы данных и начинает репликацию данных.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-125">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="ba2e4-126">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ba2e4-126">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="ba2e4-127">Получает одну или несколько баз данных.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-127">Gets one or more databases.</span></span> |
| [<span data-ttu-id="ba2e4-128">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="ba2e4-128">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="ba2e4-129">Преобразует базу данных-получатель в базу данных-источник для запуска отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-129">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="ba2e4-130">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="ba2e4-130">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="ba2e4-131">Получает связи георепликации между базой данных SQL Azure и группой ресурсов или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-131">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="ba2e4-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ba2e4-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ba2e4-133">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="ba2e4-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="ba2e4-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba2e4-134">Next steps</span></span>

<span data-ttu-id="ba2e4-135">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba2e4-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ba2e4-136">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ba2e4-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
