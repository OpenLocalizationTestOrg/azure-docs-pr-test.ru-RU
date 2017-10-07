---
title: "aaaPowerShell пример монитора шкалы SQL эластичный пул Azure базы данных SQL | Документы Microsoft"
description: "Azure PowerShell пример сценария toomonitor и масштаб гибкий пул SQL в базе данных SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="d5520-103">Используйте PowerShell toomonitor и масштабировать гибкий пул SQL в базе данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d5520-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="d5520-104">Этот пример сценария PowerShell, что мониторы hello показателей производительности пула эластичных БД масштабирует его tooa высокий уровень производительности и создает правило генерации оповещений на одном hello метрики производительности.</span><span class="sxs-lookup"><span data-stu-id="d5520-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d5520-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d5520-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d5520-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d5520-106">Clean up deployment</span></span>

<span data-ttu-id="d5520-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="d5520-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d5520-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d5520-108">Script explanation</span></span>

<span data-ttu-id="d5520-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d5520-109">This script uses hello following commands.</span></span> <span data-ttu-id="d5520-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="d5520-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d5520-111">Команда</span><span class="sxs-lookup"><span data-stu-id="d5520-111">Command</span></span> | <span data-ttu-id="d5520-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="d5520-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="d5520-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5520-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d5520-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d5520-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d5520-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="d5520-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d5520-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="d5520-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d5520-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="d5520-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="d5520-118">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="d5520-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="d5520-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d5520-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="d5520-120">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="d5520-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="d5520-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="d5520-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="d5520-122">Показывает сведения об использовании hello размер для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="d5520-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="d5520-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="d5520-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="d5520-124">Добавляет или обновляет правило генерации оповещений на основе метрики.</span><span class="sxs-lookup"><span data-stu-id="d5520-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="d5520-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="d5520-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="d5520-126">Обновляет свойства эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="d5520-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="d5520-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="d5520-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="d5520-128">Задает правило оповещения tooautomatically монитор Dtu в hello будущих.</span><span class="sxs-lookup"><span data-stu-id="d5520-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="d5520-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d5520-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d5520-130">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d5520-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d5520-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5520-131">Next steps</span></span>

<span data-ttu-id="d5520-132">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5520-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d5520-133">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d5520-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
