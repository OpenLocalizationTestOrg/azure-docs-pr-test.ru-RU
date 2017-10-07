---
title: "гибкий пул Azure SQL пример перемещения базы данных SQL aaaPowerShell | Документы Microsoft"
description: "Azure PowerShell пример сценария toomove базы данных SQL между эластичные пулы, с помощью PowerShell"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="47bda-103">Использование пулов эластичных toocreate PowerShell и перемещение между пулов эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="47bda-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="47bda-104">В этом примере сценария PowerShell создает два пула эластичных и перемещает базы данных из одного пула эластичных БД в другой пул эластичных и затем выходит уровень производительности эластичного пула tooa одной базы данных из базы данных.</span><span class="sxs-lookup"><span data-stu-id="47bda-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="47bda-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="47bda-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="47bda-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="47bda-106">Clean up deployment</span></span>

<span data-ttu-id="47bda-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="47bda-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="47bda-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="47bda-108">Script explanation</span></span>

<span data-ttu-id="47bda-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="47bda-109">This script uses hello following commands.</span></span> <span data-ttu-id="47bda-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="47bda-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="47bda-111">Команда</span><span class="sxs-lookup"><span data-stu-id="47bda-111">Command</span></span> | <span data-ttu-id="47bda-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="47bda-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="47bda-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47bda-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="47bda-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="47bda-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="47bda-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="47bda-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="47bda-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="47bda-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="47bda-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="47bda-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="47bda-118">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="47bda-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="47bda-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="47bda-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="47bda-120">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="47bda-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="47bda-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="47bda-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="47bda-122">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="47bda-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="47bda-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47bda-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="47bda-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="47bda-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="47bda-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47bda-125">Next steps</span></span>

<span data-ttu-id="47bda-126">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="47bda-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="47bda-127">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="47bda-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
