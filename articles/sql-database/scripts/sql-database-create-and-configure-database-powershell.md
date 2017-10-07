---
title: "aaaPowerShell пример создания базы данных Azure SQL | Документы Microsoft"
description: "Azure PowerShell пример сценария toocreate базы данных Azure SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="82cad-103">Используйте PowerShell toocreate одной базы данных Azure SQL и настройте правила брандмауэра</span><span class="sxs-lookup"><span data-stu-id="82cad-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="82cad-104">Этот пример сценария PowerShell создает базу данных SQL Azure и настраивает правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="82cad-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="82cad-105">После успешного выполнения сценария hello приветствия базы данных SQL может осуществляться из всех служб Azure и hello настроить IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="82cad-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="82cad-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="82cad-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="82cad-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="82cad-107">Clean up deployment</span></span>

<span data-ttu-id="82cad-108">После выполнения сценария образец hello hello, следующая команда может быть группы ресурсов используется tooremove hello и все ресурсы, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="82cad-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="82cad-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="82cad-109">Script explanation</span></span>

<span data-ttu-id="82cad-110">Этот скрипт использует hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="82cad-110">This script uses hello following commands.</span></span> <span data-ttu-id="82cad-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="82cad-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="82cad-112">Команда</span><span class="sxs-lookup"><span data-stu-id="82cad-112">Command</span></span> | <span data-ttu-id="82cad-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="82cad-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="82cad-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="82cad-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="82cad-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="82cad-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="82cad-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="82cad-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="82cad-117">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="82cad-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="82cad-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="82cad-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="82cad-119">Создает брандмауэра правило tooallow доступа tooall баз данных SQL на сервере hello из hello ввести диапазон IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="82cad-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="82cad-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="82cad-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="82cad-121">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="82cad-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="82cad-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="82cad-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="82cad-123">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="82cad-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="82cad-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82cad-124">Next steps</span></span>

<span data-ttu-id="82cad-125">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="82cad-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="82cad-126">Дополнительные примеры скриптов PowerShell базы данных SQL можно найти в hello [скриптов базы данных SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="82cad-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



