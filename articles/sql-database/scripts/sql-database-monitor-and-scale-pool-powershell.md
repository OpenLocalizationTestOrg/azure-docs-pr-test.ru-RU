---
title: "Пример для PowerShell. Мониторинг и масштабирование эластичного пула SQL в Базе данных SQL Azure | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для отслеживания и масштабирования эластичного пула SQL в Базе данных SQL Azure."
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
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="6f601-103">Отслеживание и масштабирование эластичного пула SQL в Базе данных SQL Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f601-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="6f601-104">Этот пример сценария PowerShell отслеживает метрики производительности эластичного пула, масштабирует его до более высокого уровня производительности и создает правило генерации оповещений для одной из метрик производительности.</span><span class="sxs-lookup"><span data-stu-id="6f601-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="6f601-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6f601-105">Sample script</span></span>

<span data-ttu-id="6f601-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Мониторинг и масштабирование отдельной базы данных SQL")]</span><span class="sxs-lookup"><span data-stu-id="6f601-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6f601-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="6f601-107">Clean up deployment</span></span>

<span data-ttu-id="6f601-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6f601-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="6f601-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6f601-109">Script explanation</span></span>

<span data-ttu-id="6f601-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6f601-110">This script uses the following commands.</span></span> <span data-ttu-id="6f601-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="6f601-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6f601-112">Команда</span><span class="sxs-lookup"><span data-stu-id="6f601-112">Command</span></span> | <span data-ttu-id="6f601-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="6f601-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="6f601-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6f601-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6f601-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6f601-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6f601-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="6f601-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="6f601-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="6f601-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="6f601-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="6f601-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="6f601-119">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="6f601-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="6f601-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="6f601-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="6f601-121">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="6f601-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="6f601-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="6f601-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="6f601-123">Отображает сведения об используемом размере базы данных.</span><span class="sxs-lookup"><span data-stu-id="6f601-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="6f601-124">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="6f601-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="6f601-125">Добавляет или обновляет правило генерации оповещений на основе метрики.</span><span class="sxs-lookup"><span data-stu-id="6f601-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="6f601-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="6f601-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="6f601-127">Обновляет свойства эластичного пула.</span><span class="sxs-lookup"><span data-stu-id="6f601-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="6f601-128">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="6f601-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="6f601-129">Задает правило генерации оповещений для автоматического отслеживания единиц DTU в будущем.</span><span class="sxs-lookup"><span data-stu-id="6f601-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="6f601-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6f601-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="6f601-131">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="6f601-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="6f601-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f601-132">Next steps</span></span>

<span data-ttu-id="6f601-133">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f601-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6f601-134">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6f601-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
