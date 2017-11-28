---
title: "Azure PowerShell. Создание базы данных SQL | Документация Майкрософт"
description: "Узнайте, как toocreate логический сервер базы данных SQL, правила брандмауэра уровня сервера и баз данных в hello портал Azure."
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
ms.openlocfilehash: e89f68b44083a3b64e61f95117dbbedfa6647ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-powershell"></a><span data-ttu-id="62b53-104">Создание отдельной базы данных SQL Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="62b53-104">Create a single Azure SQL database using PowerShell</span></span>

<span data-ttu-id="62b53-105">Используется toocreate и управления ресурсами Azure hello командной строке или в скриптах PowerShell.</span><span class="sxs-lookup"><span data-stu-id="62b53-105">PowerShell is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="62b53-106">Это руководство с помощью PowerShell toodeploy сведения о базе данных Azure SQL в [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) в [логический сервер базы данных SQL Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="62b53-106">This guide details using PowerShell toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="62b53-107">Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="62b53-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

<span data-ttu-id="62b53-108">Этот учебник требует hello Azure PowerShell модуль версии 4.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="62b53-108">This tutorial requires hello Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="62b53-109">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="62b53-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="62b53-110">Если требуется tooinstall или обновления, см. раздел [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="62b53-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

## <a name="log-in-tooazure"></a><span data-ttu-id="62b53-111">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="62b53-111">Log in tooAzure</span></span>

<span data-ttu-id="62b53-112">Войдите в tooyour подписку Azure с помощью hello [AzureRmAccount добавить](/powershell/module/azurerm.profile/add-azurermaccount) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="62b53-112">Log in tooyour Azure subscription using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command and follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a><span data-ttu-id="62b53-113">Создание переменных</span><span class="sxs-lookup"><span data-stu-id="62b53-113">Create variables</span></span>

<span data-ttu-id="62b53-114">Определите переменные для использования в сценариях hello в этом кратком руководстве.</span><span class="sxs-lookup"><span data-stu-id="62b53-114">Define variables for use in hello scripts in this quick start.</span></span>

```powershell
# hello data center and resource name for your resources
$resourcegroupname = "myResourceGroup"
$location = "WestEurope"
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
$servername = "server-$(Get-Random)"
# Set an admin login and password for your database
# hello login information for hello server
$adminlogin = "ServerAdmin"
$password = "ChangeYourAdminPassword1"
# hello ip address range that you want tooallow tooaccess your server - change as appropriate
$startip = "0.0.0.0"
$endip = "0.0.0.0"
# hello database name
$databasename = "mySampleDatabase"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="62b53-115">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="62b53-115">Create a resource group</span></span>

<span data-ttu-id="62b53-116">Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) команды.</span><span class="sxs-lookup"><span data-stu-id="62b53-116">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="62b53-117">Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа.</span><span class="sxs-lookup"><span data-stu-id="62b53-117">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="62b53-118">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение.</span><span class="sxs-lookup"><span data-stu-id="62b53-118">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="62b53-119">Создание логического сервера</span><span class="sxs-lookup"><span data-stu-id="62b53-119">Create a logical server</span></span>

<span data-ttu-id="62b53-120">Создание [логический сервер базы данных SQL Azure](sql-database-features.md) с помощью hello [New AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) команды.</span><span class="sxs-lookup"><span data-stu-id="62b53-120">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) command.</span></span> <span data-ttu-id="62b53-121">Логический сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="62b53-121">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="62b53-122">Hello следующий пример создает произвольным именем сервера в группе ресурсов с именем входа администратора с именем `ServerAdmin` и паролем `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="62b53-122">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="62b53-123">Замените эти предопределенные значения по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="62b53-123">Replace these pre-defined values as desired.</span></span>

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="62b53-124">Настройка правил брандмауэра сервера</span><span class="sxs-lookup"><span data-stu-id="62b53-124">Configure a server firewall rule</span></span>

<span data-ttu-id="62b53-125">Создание [правила брандмауэра уровня сервера базы данных SQL Azure](sql-database-firewall-configure.md) с помощью hello [New AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) команды.</span><span class="sxs-lookup"><span data-stu-id="62b53-125">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) command.</span></span> <span data-ttu-id="62b53-126">Правила брандмауэра уровня сервера позволяет внешнему приложению, например SQL Server Management Studio или hello SQLCMD программа tooconnect tooa SQL базы данных через брандмауэр службы hello базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="62b53-126">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="62b53-127">В следующем примере hello брандмауэр hello открыт только для других ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="62b53-127">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="62b53-128">tooenable возможности внешнего подключения, изменение hello tooan соответствующий адрес для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="62b53-128">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="62b53-129">tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="62b53-129">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> <span data-ttu-id="62b53-130">База данных SQL обменивается данными через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="62b53-130">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="62b53-131">Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 1433 может оказаться невозможным брандмауэром вашей сети.</span><span class="sxs-lookup"><span data-stu-id="62b53-131">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="62b53-132">В этом случае нельзя сервера базы данных SQL Azure может tooconnect tooyour Если ИТ-отдел открывает порт 1433.</span><span class="sxs-lookup"><span data-stu-id="62b53-132">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="62b53-133">Создайте базу данных сервера hello с образцами данных</span><span class="sxs-lookup"><span data-stu-id="62b53-133">Create a database in hello server with sample data</span></span>

<span data-ttu-id="62b53-134">Создание базы данных с [уровень производительности не ниже S0](sql-database-service-tiers.md) в hello server с помощью hello [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) команды.</span><span class="sxs-lookup"><span data-stu-id="62b53-134">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) command.</span></span> <span data-ttu-id="62b53-135">Hello следующий пример создает базу данных с именем `mySampleDatabase` и загружает hello AdventureWorksLT образец данных в эту базу данных.</span><span class="sxs-lookup"><span data-stu-id="62b53-135">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="62b53-136">В случае необходимости заменить эти предопределенные значения (другие краткие в этой сборке коллекции на hello значения в этом кратком руководстве).</span><span class="sxs-lookup"><span data-stu-id="62b53-136">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a><span data-ttu-id="62b53-137">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="62b53-137">Clean up resources</span></span>

<span data-ttu-id="62b53-138">Другие краткие руководства в этой коллекции созданы на основе этого документа.</span><span class="sxs-lookup"><span data-stu-id="62b53-138">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="62b53-139">Если планируется toocontinue toowork с последующей краткие, не очистки hello ресурсы, созданные в этом быстрого запускаются.</span><span class="sxs-lookup"><span data-stu-id="62b53-139">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="62b53-140">Если вы не планируете toocontinue, используйте следующие шаги toodelete все ресурсы, которые созданы в этом кратком руководстве в hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="62b53-140">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="62b53-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62b53-141">Next steps</span></span>

<span data-ttu-id="62b53-142">Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства.</span><span class="sxs-lookup"><span data-stu-id="62b53-142">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="62b53-143">См. дополнительные сведения о доступных средствах:</span><span class="sxs-lookup"><span data-stu-id="62b53-143">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="62b53-144">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="62b53-144">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="62b53-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="62b53-145">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="62b53-146">.NET</span><span class="sxs-lookup"><span data-stu-id="62b53-146">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="62b53-147">PHP</span><span class="sxs-lookup"><span data-stu-id="62b53-147">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="62b53-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="62b53-148">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="62b53-149">Java</span><span class="sxs-lookup"><span data-stu-id="62b53-149">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="62b53-150">Python</span><span class="sxs-lookup"><span data-stu-id="62b53-150">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="62b53-151">Ruby</span><span class="sxs-lookup"><span data-stu-id="62b53-151">Ruby</span></span>](sql-database-connect-query-ruby.md)

