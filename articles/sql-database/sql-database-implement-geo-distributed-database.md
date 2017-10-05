---
title: "Реализация решения географически распределенной базы данных SQL Azure | Документация Майкрософт"
description: "Сведения о настройке базы данных SQL Azure и приложения для отработки отказа в реплицированную базу данных и тестовой отработки отказа."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9f53f318e20dac9248906bdbe898ba4dacb286ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="e7761-103">Реализация географически распределенной базы данных</span><span class="sxs-lookup"><span data-stu-id="e7761-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="e7761-104">В этом руководстве вы настроите базу данных SQL Azure и приложение для отработки отказа в удаленный регион, а затем протестируете план отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e7761-104">In this tutorial, you configure an Azure SQL database and application for failover to a remote region, and then test your failover plan.</span></span> <span data-ttu-id="e7761-105">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e7761-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e7761-106">создавать пользователей базы данных и предоставлять им разрешения;</span><span class="sxs-lookup"><span data-stu-id="e7761-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="e7761-107">настраивать правила брандмауэра уровня базы данных;</span><span class="sxs-lookup"><span data-stu-id="e7761-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="e7761-108">создавать [группу отработки отказа георепликации](sql-database-geo-replication-overview.md);</span><span class="sxs-lookup"><span data-stu-id="e7761-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="e7761-109">создавать и компилировать приложения Java для запроса базы данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="e7761-109">Create and compile a Java application to query an Azure SQL database</span></span>
> * <span data-ttu-id="e7761-110">выполнять отработку аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="e7761-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="e7761-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="e7761-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e7761-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e7761-112">Prerequisites</span></span>

<span data-ttu-id="e7761-113">Для работы с этим руководством выполните следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="e7761-113">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="e7761-114">Установите последнюю версию [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e7761-114">Installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="e7761-115">Установите базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e7761-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="e7761-116">В этом руководстве используется пример базы данных AdventureWorksLT с именем **mySampleDatabase** из одного из этих кратких руководств:</span><span class="sxs-lookup"><span data-stu-id="e7761-116">This tutorial uses the AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="e7761-117">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="e7761-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="e7761-118">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7761-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="e7761-119">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7761-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="e7761-120">После определения метода для выполнения сценариев SQL для базы данных можно использовать одно из следующих средств запроса:</span><span class="sxs-lookup"><span data-stu-id="e7761-120">Have identified a method to execute SQL scripts against your database, you can use one of the following query tools:</span></span>
   - <span data-ttu-id="e7761-121">Редактор запросов на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7761-121">The query editor in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e7761-122">Дополнительные сведения об использовании редактора запросов на портале Azure см. в разделе [Отправка запросов к базе данных SQL](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="e7761-122">For more information on using the query editor in the Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="e7761-123">Последнюю версию [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), которая является интегрированной средой для управления любой инфраструктурой SQL, от SQL Server до базы данных SQL для Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="e7761-123">The newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server to SQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="e7761-124">Последнюю версию [Visual Studio Code](https://code.visualstudio.com/docs), которая является графическим редактором кода для Linux, macOS и Windows, поддерживающим различные расширения, включая [расширение mssql](https://aka.ms/mssql-marketplace), для выполнения запросов к Microsoft SQL Server, базе данных SQL Azure и хранилищу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e7761-124">The newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="e7761-125">Дополнительные сведения об использовании этого средства в базе данных SQL Azure см. в статье [База данных SQL Azure: подключение и запрос данных с помощью Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="e7761-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="e7761-126">Создание пользователей базы данных и предоставление им разрешений</span><span class="sxs-lookup"><span data-stu-id="e7761-126">Create database users and grant permissions</span></span>

<span data-ttu-id="e7761-127">Подключитесь к базе данных и создайте учетные записи пользователей с помощью одного из следующих средств запроса:</span><span class="sxs-lookup"><span data-stu-id="e7761-127">Connect to your database and create user accounts using one of the following query tools:</span></span>

- <span data-ttu-id="e7761-128">редактора запросов на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="e7761-128">The Query editor in the Azure portal</span></span>
- <span data-ttu-id="e7761-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="e7761-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="e7761-130">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="e7761-130">Visual Studio Code</span></span>

<span data-ttu-id="e7761-131">Эти учетные записи пользователей автоматически реплицируются на сервер-получатель (синхронизация обязательна).</span><span class="sxs-lookup"><span data-stu-id="e7761-131">These user accounts replicate automatically to your secondary server (and be kept in sync).</span></span> <span data-ttu-id="e7761-132">Чтобы использовать SQL Server Management Studio или Visual Studio Code, вам может потребоваться настроить правило брандмауэра при подключении из клиента по IP-адресу, для которого еще не настроен брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="e7761-132">To use SQL Server Management Studio or Visual Studio Code, you may need to configure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="e7761-133">Подробные инструкции см. в разделе [Создание правила брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="e7761-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="e7761-134">Чтобы создать в базе данных две учетные записи пользователя, в окне запроса выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="e7761-134">In a query window, execute the following query to create two user accounts in your database.</span></span> <span data-ttu-id="e7761-135">Этот скрипт предоставляет разрешения **db_owner** для учетной записи **app_admin**, а также разрешения **SELECT** и **UPDATE** для учетной записи **app_user**.</span><span class="sxs-lookup"><span data-stu-id="e7761-135">This script grants **db_owner** permissions to the **app_admin** account and grants **SELECT** and **UPDATE** permissions to the **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user to db_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission to SalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product TO app_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="e7761-136">Создание брандмауэра на уровне базы данных</span><span class="sxs-lookup"><span data-stu-id="e7761-136">Create database-level firewall</span></span>

<span data-ttu-id="e7761-137">Создайте [правило брандмауэра уровня базы данных](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e7761-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="e7761-138">Оно автоматически реплицируется на сервер-получатель, созданный в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="e7761-138">This database-level firewall rule replicates automatically to the secondary server that you create in this tutorial.</span></span> <span data-ttu-id="e7761-139">Для удобства (в рамках этого руководства) используйте общедоступный IP-адрес компьютера, на котором выполняются действия из этого руководства.</span><span class="sxs-lookup"><span data-stu-id="e7761-139">For simplicity (in this tutorial), use the public IP address of the computer on which you are performing the steps in this tutorial.</span></span> <span data-ttu-id="e7761-140">Ознакомьтесь с разделом [Создание правила брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule), чтобы определить IP-адрес, используемый для правила брандмауэра уровня сервера для текущего компьютера.</span><span class="sxs-lookup"><span data-stu-id="e7761-140">To determine the IP address used for the server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="e7761-141">В открытом окне запроса замените предыдущий запрос следующим запросом, указав соответствующие IP-адреса для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e7761-141">In your open query window, replace the previous query with the following query, replacing the IP addresses with the appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="e7761-142">Создание группы автоматической отработки отказа и активная георепликация</span><span class="sxs-lookup"><span data-stu-id="e7761-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="e7761-143">С помощью Azure PowerShell создайте [группу автоматической отработки отказа активной георепликации](sql-database-geo-replication-overview.md) между существующим сервером SQL Azure и новым пустым сервером SQL Azure в регионе Azure, а затем добавьте пример базы данных в группу отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e7761-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and the new empty Azure SQL server in an Azure region, and then add your sample database to the failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7761-144">Для выполнения этих командлетов требуется Azure PowerShell версии 4.0.</span><span class="sxs-lookup"><span data-stu-id="e7761-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="e7761-145">Заполните переменные для сценариев PowerShell, используя значения для имеющегося сервера и примера базы данных, а также присвойте имени группы отработки отказа глобальное уникальное значение.</span><span class="sxs-lookup"><span data-stu-id="e7761-145">Populate variables for your PowerShell scripts using the values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="e7761-146">Создайте пустой резервный сервер в вашем регионе отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e7761-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="e7761-147">Создайте группу отработки отказа между двумя серверами.</span><span class="sxs-lookup"><span data-stu-id="e7761-147">Create a failover group between the two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="e7761-148">Добавьте базу данных в группу отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e7761-148">Add your database to the failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="e7761-149">Установка программного обеспечения Java</span><span class="sxs-lookup"><span data-stu-id="e7761-149">Install Java software</span></span>

<span data-ttu-id="e7761-150">В этом разделе предполагается, что у вас уже есть опыт разработки на Java и вы только начали работу с Базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e7761-150">The steps in this section assume that you are familiar with developing using Java and are new to working with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="e7761-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="e7761-151">**Mac OS**</span></span>
<span data-ttu-id="e7761-152">Откройте терминал и перейдите в каталог, в котором вы планируете создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="e7761-152">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="e7761-153">Введите следующие команды для установки **brew** и **Maven**.</span><span class="sxs-lookup"><span data-stu-id="e7761-153">Install **brew** and **Maven** by entering the following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="e7761-154">Для получения подробных инструкций по установке и настройке сред Java и Maven перейдите на ресурс [создания приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), выберите **Java**, затем — **MacOS** и выполните подробные инструкции по настройке Java и Maven (шаги 1.2 и 1.3).</span><span class="sxs-lookup"><span data-stu-id="e7761-154">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="e7761-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="e7761-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="e7761-156">Откройте терминал и перейдите в каталог, в котором вы планируете создать проект Java.</span><span class="sxs-lookup"><span data-stu-id="e7761-156">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="e7761-157">Введите следующие команды для установки **Maven**.</span><span class="sxs-lookup"><span data-stu-id="e7761-157">Install **Maven** by entering the following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="e7761-158">Для получения подробных инструкций по установке и настройке сред Java и Maven перейдите на ресурс [создания приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), выберите **Java**, затем — **Ubuntu** и выполните подробные инструкции по настройке Java и Maven (шаги 1.2, 1.3 и 1.4).</span><span class="sxs-lookup"><span data-stu-id="e7761-158">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow the detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="e7761-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="e7761-159">**Windows**</span></span>
<span data-ttu-id="e7761-160">Установите [Maven](https://maven.apache.org/download.cgi) с помощью официального установщика.</span><span class="sxs-lookup"><span data-stu-id="e7761-160">Install [Maven](https://maven.apache.org/download.cgi) using the official installer.</span></span> <span data-ttu-id="e7761-161">Maven можно использовать для управления зависимостями, выполнения сборки, тестирования и запуска проекта Java.</span><span class="sxs-lookup"><span data-stu-id="e7761-161">Use Maven to help manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="e7761-162">Для получения подробных инструкций по установке и настройке сред Java и Maven перейдите на ресурс [создания приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), выберите **Java**, затем — Windows и выполните подробные инструкции по настройке Java и Maven (шаги 1.2 и 1.3).</span><span class="sxs-lookup"><span data-stu-id="e7761-162">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="e7761-163">Создание проекта SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="e7761-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="e7761-164">В окне командной консоли (например, Bash) создайте проект Maven.</span><span class="sxs-lookup"><span data-stu-id="e7761-164">In the command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="e7761-165">Введите **Y** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="e7761-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="e7761-166">Перейдите в только что созданный проект.</span><span class="sxs-lookup"><span data-stu-id="e7761-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="e7761-167">Используя любой удобный редактор, откройте файл pom.xml в папке проекта.</span><span class="sxs-lookup"><span data-stu-id="e7761-167">Using your favorite editor, open the pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="e7761-168">Добавьте Microsoft JDBC Driver для зависимости SQL Server в проект Maven. Для этого откройте удобный текстовый редактор, скопируйте и вставьте следующие строки в файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="e7761-168">Add the Microsoft JDBC Driver for SQL Server dependency to your Maven project by opening your favorite text editor and copying and pasting the following lines into your pom.xml file.</span></span> <span data-ttu-id="e7761-169">Не перезаписывайте имеющиеся значения, предварительно заполненные в файле.</span><span class="sxs-lookup"><span data-stu-id="e7761-169">Do not overwrite the existing values prepopulated in the file.</span></span> <span data-ttu-id="e7761-170">JDBC-зависимость необходимо вставить в рамках большего раздела зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e7761-170">The JDBC dependency must be pasted within the larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="e7761-171">Укажите версию Java, с помощью которой нужно скомпилировать проект. Для этого добавьте следующий раздел свойств в файл pom.xml после раздела зависимостей.</span><span class="sxs-lookup"><span data-stu-id="e7761-171">Specify the version of Java to compile the project against by adding the following “properties” section into the pom.xml file after the "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="e7761-172">Добавьте следующий раздел сборки в файл pom.xml после раздела свойств для поддержки файлов манифеста в JAR-файлах.</span><span class="sxs-lookup"><span data-stu-id="e7761-172">Add the following "build" section into the pom.xml file after the "properties" section to support manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="e7761-173">Сохраните и закройте файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="e7761-173">Save and close the pom.xml file.</span></span>
9. <span data-ttu-id="e7761-174">Откройте файл App.java (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) и замените его содержимое на содержимое ниже.</span><span class="sxs-lookup"><span data-stu-id="e7761-174">Open the App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace the contents with the following contents.</span></span> <span data-ttu-id="e7761-175">Замените имя группы отработки отказа на имя своей группы отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e7761-175">Replace the failover group name with the name for your failover group.</span></span> <span data-ttu-id="e7761-176">Если вы изменили значения для имени базы данных, пользователя или пароля, измените также эти значения.</span><span class="sxs-lookup"><span data-stu-id="e7761-176">If you have changed the values for the database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into the product table with a unique product name that we can use to find the product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query the data that was previously inserted into the primary database from the geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query the high water mark id that is stored in the table to be able to make unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="e7761-177">Сохраните и закройте файл App.java.</span><span class="sxs-lookup"><span data-stu-id="e7761-177">Save and close the App.java file.</span></span>

## <a name="compile-and-run-the-sqldbsample-project"></a><span data-ttu-id="e7761-178">Компиляция и выполнение проекта SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="e7761-178">Compile and run the SqlDbSample project</span></span>

1. <span data-ttu-id="e7761-179">В окне командной консоли выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e7761-179">In the command console, execute to following command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="e7761-180">После завершения выполните следующую команду для запуска приложения (запуск выполняется около часа, если не завершить эту задачу вручную):</span><span class="sxs-lookup"><span data-stu-id="e7761-180">When finished, execute the following command to run the application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="e7761-181">Выполнение отработки аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="e7761-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="e7761-182">Для группы отработки отказа вызовите отработку отказа вручную.</span><span class="sxs-lookup"><span data-stu-id="e7761-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="e7761-183">Просмотрите результаты приложения во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e7761-183">Observe the application results during failover.</span></span> <span data-ttu-id="e7761-184">Во время обновления кэша DNS некоторые операции вставки завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="e7761-184">Some inserts fail while the DNS cache refreshes.</span></span>     

3. <span data-ttu-id="e7761-185">Узнайте, какую роль выполняет сервер аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="e7761-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="e7761-186">Восстановите размещение.</span><span class="sxs-lookup"><span data-stu-id="e7761-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="e7761-187">Просмотрите результаты приложения во время восстановления размещения.</span><span class="sxs-lookup"><span data-stu-id="e7761-187">Observe the application results during failback.</span></span> <span data-ttu-id="e7761-188">Во время обновления кэша DNS некоторые операции вставки завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="e7761-188">Some inserts fail while the DNS cache refreshes.</span></span>     

6. <span data-ttu-id="e7761-189">Узнайте, какую роль выполняет сервер аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="e7761-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="e7761-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7761-190">Next steps</span></span> 

<span data-ttu-id="e7761-191">Дополнительные сведения см. в статье [Обзор. Группы отработки отказа и активная георепликация](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7761-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
