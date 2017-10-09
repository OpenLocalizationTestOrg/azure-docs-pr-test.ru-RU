---
title: "База данных Azure SQL географическая репликация пула пример активный aaaPowerShell | Документы Microsoft"
description: "Azure PowerShell пример сценария tooset копирование активной георепликации для пула базы данных Azure SQL"
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
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="c8e6f-103">Используйте PowerShell tooconfigure активной георепликации для пула базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="c8e6f-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="c8e6f-104">В этом примере сценария PowerShell настраивает активной георепликации для базы данных Azure SQL в пуле эластичных БД и отказа toohello вторичной реплики базы данных Azure SQL hello.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="c8e6f-105">Примеры сценариев</span><span class="sxs-lookup"><span data-stu-id="c8e6f-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c8e6f-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c8e6f-106">Clean up deployment</span></span>

<span data-ttu-id="c8e6f-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c8e6f-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c8e6f-108">Script explanation</span></span>

<span data-ttu-id="c8e6f-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-109">This script uses hello following commands.</span></span> <span data-ttu-id="c8e6f-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c8e6f-111">Команда</span><span class="sxs-lookup"><span data-stu-id="c8e6f-111">Command</span></span> | <span data-ttu-id="c8e6f-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="c8e6f-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c8e6f-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c8e6f-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c8e6f-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c8e6f-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c8e6f-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="c8e6f-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c8e6f-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="c8e6f-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="c8e6f-118">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="c8e6f-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c8e6f-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="c8e6f-120">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="c8e6f-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c8e6f-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="c8e6f-122">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="c8e6f-123">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="c8e6f-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="c8e6f-124">Создает базу данных-получатель для существующей базы данных и начинает репликацию данных.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="c8e6f-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c8e6f-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="c8e6f-126">Получает одну или несколько баз данных.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="c8e6f-127">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="c8e6f-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="c8e6f-128">Переключает toobe основной базы данных-получателя в tooinitiate порядок перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="c8e6f-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="c8e6f-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="c8e6f-130">Получает ссылки hello географическую репликацию данных между базы данных SQL Azure и группы ресурсов или SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="c8e6f-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c8e6f-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c8e6f-132">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c8e6f-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c8e6f-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8e6f-133">Next steps</span></span>

<span data-ttu-id="c8e6f-134">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c8e6f-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c8e6f-135">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c8e6f-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
