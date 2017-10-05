---
title: "Пример для PowerShell. Перемещение базы данных SQL Azure в эластичный пул SQL | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для перемещения базы данных SQL между эластичными пулами."
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
ms.openlocfilehash: 58f14dc668f25f17e93fcaf30f72b15a46d71484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-create-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="f7aa3-103">Создание эластичных пулов и перемещение баз данных между эластичными пулами с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7aa3-103">Use PowerShell to create elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="f7aa3-104">Этот пример сценария PowerShell создает два эластичных пула и перемещает базу данных из одного пула в другой, а затем перемещает базу данных из этого эластичного пула на уровень производительности отдельной базы данных.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f7aa3-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="f7aa3-105">Sample script</span></span>

<span data-ttu-id="f7aa3-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Перемещение базы данных между пулами")]</span><span class="sxs-lookup"><span data-stu-id="f7aa3-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f7aa3-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="f7aa3-107">Clean up deployment</span></span>

<span data-ttu-id="f7aa3-108">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f7aa3-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="f7aa3-109">Script explanation</span></span>

<span data-ttu-id="f7aa3-110">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-110">This script uses the following commands.</span></span> <span data-ttu-id="f7aa3-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f7aa3-112">Команда</span><span class="sxs-lookup"><span data-stu-id="f7aa3-112">Command</span></span> | <span data-ttu-id="f7aa3-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="f7aa3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f7aa3-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7aa3-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f7aa3-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f7aa3-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="f7aa3-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f7aa3-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f7aa3-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="f7aa3-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="f7aa3-119">Создает эластичный пул на логическом сервере.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="f7aa3-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f7aa3-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f7aa3-121">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f7aa3-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f7aa3-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="f7aa3-123">Обновляет свойства базы данных или перемещает базу данных в эластичный пул, из него или между эластичными пулами.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="f7aa3-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f7aa3-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f7aa3-125">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f7aa3-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f7aa3-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7aa3-126">Next steps</span></span>

<span data-ttu-id="f7aa3-127">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f7aa3-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f7aa3-128">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f7aa3-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
