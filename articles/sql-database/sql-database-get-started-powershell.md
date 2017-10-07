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
# <a name="create-a-single-azure-sql-database-using-powershell"></a>Создание отдельной базы данных SQL Azure с помощью PowerShell

Используется toocreate и управления ресурсами Azure hello командной строке или в скриптах PowerShell. Это руководство с помощью PowerShell toodeploy сведения о базе данных Azure SQL в [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) в [логический сервер базы данных SQL Azure](sql-database-features.md).

Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.

Этот учебник требует hello Azure PowerShell модуль версии 4.0 или более поздней версии. Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps). 

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Войдите в tooyour подписку Azure с помощью hello [AzureRmAccount добавить](/powershell/module/azurerm.profile/add-azurermaccount) команды и выполните hello на экране инструкциям.

```powershell
Add-AzureRmAccount
```

## <a name="create-variables"></a>Создание переменных

Определите переменные для использования в сценариях hello в этом кратком руководстве.

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

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание [группы ресурсов Azure](../azure-resource-manager/resource-group-overview.md) с помощью hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) команды. Группа ресурсов — это логический контейнер, в котором ресурсы Azure развертываются и администрируются как группа. Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение.

```powershell
New-AzureRmResourceGroup -Name $resourcegroupname -Location $location
```
## <a name="create-a-logical-server"></a>Создание логического сервера

Создание [логический сервер базы данных SQL Azure](sql-database-features.md) с помощью hello [New AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) команды. Логический сервер содержит группу баз данных, которыми можно управлять как группой. Hello следующий пример создает произвольным именем сервера в группе ресурсов с именем входа администратора с именем `ServerAdmin` и паролем `ChangeYourAdminPassword1`. Замените эти предопределенные значения по своему усмотрению.

```powershell
New-AzureRmSqlServer -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -Location $location `
    -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
```

## <a name="configure-a-server-firewall-rule"></a>Настройка правил брандмауэра сервера

Создание [правила брандмауэра уровня сервера базы данных SQL Azure](sql-database-firewall-configure.md) с помощью hello [New AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) команды. Правила брандмауэра уровня сервера позволяет внешнему приложению, например SQL Server Management Studio или hello SQLCMD программа tooconnect tooa SQL базы данных через брандмауэр службы hello базы данных SQL. В следующем примере hello брандмауэр hello открыт только для других ресурсов Azure. tooenable возможности внешнего подключения, изменение hello tooan соответствующий адрес для вашей среды. tooopen всех IP-адресов, использовать в качестве hello, начальный IP-адрес и 255.255.255.255 как hello конечный адрес 0.0.0.0.

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress $startip -EndIpAddress $endip
```

> [!NOTE]
> База данных SQL обменивается данными через порт 1433. Если вы пытаетесь tooconnect из корпоративной сети, исходящий трафик через порт 1433 может оказаться невозможным брандмауэром вашей сети. В этом случае нельзя сервера базы данных SQL Azure может tooconnect tooyour Если ИТ-отдел открывает порт 1433.
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a>Создайте базу данных сервера hello с образцами данных

Создание базы данных с [уровень производительности не ниже S0](sql-database-service-tiers.md) в hello server с помощью hello [New AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) команды. Hello следующий пример создает базу данных с именем `mySampleDatabase` и загружает hello AdventureWorksLT образец данных в эту базу данных. В случае необходимости заменить эти предопределенные значения (другие краткие в этой сборке коллекции на hello значения в этом кратком руководстве).

```powershell
New-AzureRmSqlDatabase  -ResourceGroupName $resourcegroupname `
    -ServerName $servername `
    -DatabaseName $databasename `
    -SampleName "AdventureWorksLT" `
    -RequestedServiceObjectiveName "S0"
```

## <a name="clean-up-resources"></a>Очистка ресурсов

Другие краткие руководства в этой коллекции созданы на основе этого документа. 

> [!TIP]
> Если планируется toocontinue toowork с последующей краткие, не очистки hello ресурсы, созданные в этом быстрого запускаются. Если вы не планируете toocontinue, используйте следующие шаги toodelete все ресурсы, которые созданы в этом кратком руководстве в hello портал Azure hello.
>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда у вас есть база данных, вы можете подключиться и создать запрос, используя привычные средства. См. дополнительные сведения о доступных средствах:

- [SQL Server Management Studio](sql-database-connect-query-ssms.md)
- [Visual Studio Code](sql-database-connect-query-vscode.md)
- [.NET](sql-database-connect-query-dotnet.md)
- [PHP](sql-database-connect-query-php.md)
- [Node.js](sql-database-connect-query-nodejs.md)
- [Java](sql-database-connect-query-java.md)
- [Python](sql-database-connect-query-python.md)
- [Ruby](sql-database-connect-query-ruby.md)

