---
title: "Azure PowerShell. Создание базы данных SQL | Документация Майкрософт"
description: "Вы узнаете, как создать логический сервер базы данных SQL, правило брандмауэра на уровне сервера и базы данных на портале Azure,"
keywords: "руководство по базам данных SQL, создание базы данных SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 44ed4a603977617c898315c4fc0b2d3dd3a8f16a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="ba58d-104">Создание отдельной базы данных SQL Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba58d-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="ba58d-105">PowerShell используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="ba58d-105">PowerShell is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="ba58d-106">В этом руководстве подробно описывается, как с помощью PowerShell развернуть базу данных SQL Azure в [группе ресурсов Azure](../azure-resource-manager/resource-group-overview.md) на [логическом сервере базы данных Azure SQL](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="ba58d-106">This guide details using PowerShell to deploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="ba58d-107">Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="ba58d-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="ba58d-108">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 4.0.</span><span class="sxs-lookup"><span data-stu-id="ba58d-108">This tutorial requires the Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="ba58d-109">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="ba58d-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="ba58d-110">Если вам необходимо выполнить установку или обновление, см. статью [об установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ba58d-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="ba58d-111">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="ba58d-111">Log in to Azure</span></span>

<span data-ttu-id="ba58d-112">С помощью команды [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) войдите в подписку Azure и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="ba58d-112">Log in to your Azure subscription using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="ba58d-113">Создание переменных</span><span class="sxs-lookup"><span data-stu-id="ba58d-113">Create variables</span></span>

<span data-ttu-id="ba58d-114">Определите переменные для использования в скриптах этого руководства.</span><span class="sxs-lookup"><span data-stu-id="ba58d-114">Define variables for use in the scripts in this quick start.</span></span>

```powershell
# The data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# The logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# The login information for the server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# The ip address range that you want to allow to access your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# The database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="ba58d-115">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ba58d-115">Create a resource group</span></span>

<span data-ttu-id="ba58d-116">Создайте [группу ресурсов Azure ](../azure-resource-manager/resource-group-overview.md) с помощью команды [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="ba58d-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="ba58d-117">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="ba58d-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="ba58d-118">В следующем примере создается группа ресурсов с именем `myResourceGroup` в расположении `westeurope`.</span><span class="sxs-lookup"><span data-stu-id="ba58d-118">The following example creates a resource group named `myResourceGroup` in the `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="ba58d-119">Создание логического сервера</span><span class="sxs-lookup"><span data-stu-id="ba58d-119">Create a logical server</span></span>

<span data-ttu-id="ba58d-120">Создайте [логический сервер базы данных Azure SQL](sql-database-features.md) с помощью команды [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver).</span><span class="sxs-lookup"><span data-stu-id="ba58d-120">Create an [Azure SQL Database logical server](sql-database-features.md) using the [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="ba58d-121">Логический сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="ba58d-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="ba58d-122">В примере ниже показано создание сервера со случайным именем в группе ресурсов с именем администратора `ServerAdmin` и паролем `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="ba58d-122">The following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="ba58d-123">Замените эти предопределенные значения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="ba58d-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="ba58d-124">Настройка правил брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="ba58d-124">Configure a server firewall rule</span></span>

<span data-ttu-id="ba58d-125">Создайте [правило брандмауэра на уровне сервера базы данных Azure SQL](sql-database-firewall-configure.md) с помощью команды [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule).</span><span class="sxs-lookup"><span data-stu-id="ba58d-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using the [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="ba58d-126">Правило брандмауэра на уровне сервера позволяет внешним приложениям, таким как SQL Server Management Studio или программе sqlcmd, подключаться к базе данных SQL через брандмауэр службы базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="ba58d-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or the SQLCMD utility to connect to a SQL database through the SQL Database service firewall.</span></span> <span data-ttu-id="ba58d-127">В следующем примере брандмауэр открыт только для других ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ba58d-127">In the following example, the firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="ba58d-128">Чтобы включить возможность внешнего подключения, измените IP-адрес на соответствующий адрес своей среды.</span><span class="sxs-lookup"><span data-stu-id="ba58d-128">To enable external connectivity, change the IP address to an appropriate address for your environment.</span></span> <span data-ttu-id="ba58d-129">Чтобы открыть все IP-адреса, используйте 0.0.0.0 как начальный IP-адрес, а 255.255.255.255 — как конечный.</span><span class="sxs-lookup"><span data-stu-id="ba58d-129">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="ba58d-130">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="ba58d-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="ba58d-131">Если вы пытаетесь подключиться из корпоративной сети, исходящий трафик через порт 1433 может быть запрещен сетевым брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="ba58d-131">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="ba58d-132">В таком случае вы не сможете подключиться к серверу базы данных SQL Azure. Для этого ваш ИТ-отдел должен открыть порт 1433.</span><span class="sxs-lookup"><span data-stu-id="ba58d-132">If so, you will not be able to connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-the-server-with-sample-data"></a><span data-ttu-id="ba58d-133">Создание базы данных на сервере с образцами данных</span><span class="sxs-lookup"><span data-stu-id="ba58d-133">Create a database in the server with sample data</span></span>

<span data-ttu-id="ba58d-134">С помощью команды [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) создайте на сервере базу данных с [уровнем производительности S0](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="ba58d-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in the server using the [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="ba58d-135">В следующем примере создается база данных с именем `mySampleDatabase`, в которую загружается образец данных AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="ba58d-135">The following example creates a database called `mySampleDatabase` and loads the AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="ba58d-136">При необходимости замените эти предопределенные значения (другие краткие руководства в этой коллекции созданы на основе этого документа).</span><span class="sxs-lookup"><span data-stu-id="ba58d-136">Replace these predefined values as desired (other quick starts in this collection build upon the values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="ba58d-137">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="ba58d-137">Clean up resources</span></span>

<span data-ttu-id="ba58d-138">Другие краткие руководства в этой коллекции созданы на основе этого документа.</span><span class="sxs-lookup"><span data-stu-id="ba58d-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="ba58d-139">Если вы планируете продолжать работу с этими краткими руководствами, не удаляйте созданные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ba58d-139">If you plan to continue on to work with subsequent quick starts, do not clean up the resources created in this quick start.</span></span> <span data-ttu-id="ba58d-140">Если вы не планируете продолжать работу, удалите все созданные ресурсы, выполнив на портале Azure следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ba58d-140">If you do not plan to continue, use the following steps to delete all resources created by this quick start in the Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="ba58d-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba58d-141">Next steps</span></span>

<span data-ttu-id="ba58d-142">Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства.</span><span class="sxs-lookup"><span data-stu-id="ba58d-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="ba58d-143">См. дополнительные сведения о доступных средствах:</span><span class="sxs-lookup"><span data-stu-id="ba58d-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="ba58d-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="ba58d-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="ba58d-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ba58d-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="ba58d-146">.NET</span><span class="sxs-lookup"><span data-stu-id="ba58d-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="ba58d-147">PHP</span><span class="sxs-lookup"><span data-stu-id="ba58d-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="ba58d-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="ba58d-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="ba58d-149">Java</span><span class="sxs-lookup"><span data-stu-id="ba58d-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="ba58d-150">Python</span><span class="sxs-lookup"><span data-stu-id="ba58d-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="ba58d-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="ba58d-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

