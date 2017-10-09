---
title: "SQL server aaaPowerShell пример копирования Azure для новой базы данных | Документы Microsoft"
description: "Azure PowerShell пример сценария toocopy новый сервер tooa базы данных SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="63de6-103">Используйте PowerShell toocopy новый сервер tooa базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="63de6-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="63de6-104">Этот пример сценария PowerShell создает копию существующей базы данных на новом сервере.</span><span class="sxs-lookup"><span data-stu-id="63de6-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="63de6-105">Скопируйте новый сервер базы данных tooa</span><span class="sxs-lookup"><span data-stu-id="63de6-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="63de6-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="63de6-106">Clean up deployment</span></span>

<span data-ttu-id="63de6-107">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="63de6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="63de6-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="63de6-108">Script explanation</span></span>

<span data-ttu-id="63de6-109">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="63de6-109">This script uses hello following commands.</span></span> <span data-ttu-id="63de6-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="63de6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="63de6-111">Команда</span><span class="sxs-lookup"><span data-stu-id="63de6-111">Command</span></span> | <span data-ttu-id="63de6-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="63de6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="63de6-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="63de6-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="63de6-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="63de6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="63de6-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="63de6-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="63de6-116">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="63de6-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="63de6-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="63de6-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="63de6-118">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="63de6-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="63de6-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="63de6-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="63de6-120">Создает копию базы данных, которая использует моментальный снимок hello в hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="63de6-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="63de6-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="63de6-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="63de6-122">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="63de6-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="63de6-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63de6-123">Next steps</span></span>

<span data-ttu-id="63de6-124">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63de6-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="63de6-125">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="63de6-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
