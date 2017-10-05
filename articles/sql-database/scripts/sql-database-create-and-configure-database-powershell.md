---
title: "Пример для PowerShell. Создание базы данных SQL Azure | Документация Майкрософт"
description: "Пример сценария Azure PowerShell для создания базы данных SQL Azure."
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
ms.openlocfilehash: 1b6809007e6717b7f8847452b2fa5b38d4ab5ccc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="78389-103">Создание отдельной базы данных SQL и настройка правила брандмауэра с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="78389-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="78389-104">Этот пример сценария PowerShell создает базу данных SQL Azure и настраивает правило брандмауэра уровня сервера.</span><span class="sxs-lookup"><span data-stu-id="78389-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="78389-105">После успешного выполнения скрипта доступ к базе данных SQL можно получить из всех служб Azure, а также по настроенному IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="78389-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="78389-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="78389-106">Sample script</span></span>

<span data-ttu-id="78389-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Создание базы данных SQL")]</span><span class="sxs-lookup"><span data-stu-id="78389-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="78389-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="78389-108">Clean up deployment</span></span>

<span data-ttu-id="78389-109">После выполнения примера сценария можно удалить группу ресурсов и все связанные с ней ресурсы, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="78389-109">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="78389-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="78389-110">Script explanation</span></span>

<span data-ttu-id="78389-111">Этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="78389-111">This script uses the following commands.</span></span> <span data-ttu-id="78389-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="78389-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="78389-113">Команда</span><span class="sxs-lookup"><span data-stu-id="78389-113">Command</span></span> | <span data-ttu-id="78389-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="78389-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="78389-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="78389-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="78389-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="78389-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="78389-117">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="78389-117">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="78389-118">Создает логический сервер, на котором размещена база данных или эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="78389-118">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="78389-119">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="78389-119">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="78389-120">Создает правило брандмауэра, чтобы разрешить доступ ко всем базам данных SQL на сервере по введенному диапазону IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="78389-120">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="78389-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="78389-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="78389-122">Создает на логическом сервере отдельную базу данных или базу данных в составе пула.</span><span class="sxs-lookup"><span data-stu-id="78389-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="78389-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="78389-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="78389-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="78389-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="78389-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78389-125">Next steps</span></span>

<span data-ttu-id="78389-126">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="78389-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="78389-127">Дополнительные примеры сценариев PowerShell для базы данных SQL Azure можно найти [здесь](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="78389-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



