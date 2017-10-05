---
title: "Пример для PowerShell. Группа отработки отказа георепликации для отдельной базы данных SQL Azure | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для настройки активной георепликации отдельной базы данных SQL Azure"
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
ms.openlocfilehash: 8db8540d9c4caeb53ea8f34d45d9498496d2b8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-an-active-geo-replication-failover-group-for-a-single-azure-sql-database"></a><span data-ttu-id="50cd4-103">Использование PowerShell для настройки группы отработки отказа активной георепликации для отдельной базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="50cd4-103">Use PowerShell to configure an active geo-replication failover group for a single Azure SQL database</span></span>

<span data-ttu-id="50cd4-104">Этот пример скрипта PowerShell настраивает группу отработки отказа активной георепликации для отдельной базы данных SQL Azure и выполняет для нее отработку отказа во вторичную реплику базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="50cd4-104">This PowerShell script example configures an active geo-replication failover group for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="50cd4-105">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="50cd4-105">Sample scripts</span></span>

<span data-ttu-id="50cd4-106">[!code-powershell[основной](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Настройка группы отработки отказа для отдельной базы данных")]</span><span class="sxs-lookup"><span data-stu-id="50cd4-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database-failover-group.ps1?highlight=19-22 "Set up failover group for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="50cd4-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="50cd4-107">Clean up deployment</span></span>

<span data-ttu-id="50cd4-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="50cd4-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="50cd4-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="50cd4-109">Script explanation</span></span>

<span data-ttu-id="50cd4-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="50cd4-110">This script uses the following commands.</span></span> <span data-ttu-id="50cd4-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="50cd4-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="50cd4-112">Команда</span><span class="sxs-lookup"><span data-stu-id="50cd4-112">Command</span></span> | <span data-ttu-id="50cd4-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="50cd4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50cd4-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="50cd4-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="50cd4-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="50cd4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="50cd4-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="50cd4-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="50cd4-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="50cd4-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="50cd4-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="50cd4-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="50cd4-119">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="50cd4-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="50cd4-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="50cd4-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="50cd4-121">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="50cd4-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="50cd4-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="50cd4-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="50cd4-123">Создает базу данных-получатель для существующей базы данных и начинает репликацию данных.</span><span class="sxs-lookup"><span data-stu-id="50cd4-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="50cd4-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="50cd4-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="50cd4-125">Получает одну или несколько баз данных.</span><span class="sxs-lookup"><span data-stu-id="50cd4-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="50cd4-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="50cd4-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="50cd4-127">Преобразует базу данных-получатель в базу данных-источник для запуска отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="50cd4-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="50cd4-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="50cd4-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="50cd4-129">Получает связи георепликации между базой данных SQL Azure и группой ресурсов или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="50cd4-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="50cd4-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="50cd4-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="50cd4-131">Завершает репликацию данных между базой данных SQL и указанной базой данных-получателем.</span><span class="sxs-lookup"><span data-stu-id="50cd4-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="50cd4-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="50cd4-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="50cd4-133">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="50cd4-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="50cd4-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50cd4-134">Next steps</span></span>

<span data-ttu-id="50cd4-135">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50cd4-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="50cd4-136">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="50cd4-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
