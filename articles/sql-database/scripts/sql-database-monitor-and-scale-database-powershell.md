---
title: "базы данных Azure SQL в пример монитора шкалы одним aaaPowerShell | Документы Microsoft"
description: "Azure PowerShell пример сценария toomonitor и масштаб одной базы данных Azure SQL"
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="686a8-103">Используйте PowerShell toomonitor и масштабировать одной базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="686a8-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="686a8-104">Этот пример сценария PowerShell, что мониторы hello метрики производительности базы данных, выполняет масштабирование tooa высокий уровень производительности и создает правило генерации оповещений на одном hello метрики производительности.</span><span class="sxs-lookup"><span data-stu-id="686a8-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="686a8-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="686a8-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="686a8-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="686a8-106">Clean up deployment</span></span>

<span data-ttu-id="686a8-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="686a8-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="686a8-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="686a8-108">Script explanation</span></span>

<span data-ttu-id="686a8-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="686a8-109">This script uses hello following commands.</span></span> <span data-ttu-id="686a8-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="686a8-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="686a8-111">Команда</span><span class="sxs-lookup"><span data-stu-id="686a8-111">Command</span></span> | <span data-ttu-id="686a8-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="686a8-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="686a8-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="686a8-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="686a8-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="686a8-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="686a8-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="686a8-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="686a8-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="686a8-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="686a8-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="686a8-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="686a8-118">Показывает сведения об использовании hello размер для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="686a8-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="686a8-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="686a8-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="686a8-120">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="686a8-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="686a8-121">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="686a8-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="686a8-122">Задает правило оповещения tooautomatically монитор Dtu в hello будущих.</span><span class="sxs-lookup"><span data-stu-id="686a8-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="686a8-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="686a8-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="686a8-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="686a8-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="686a8-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="686a8-125">Next steps</span></span>

<span data-ttu-id="686a8-126">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="686a8-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="686a8-127">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="686a8-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
