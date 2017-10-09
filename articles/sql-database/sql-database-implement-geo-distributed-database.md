---
title: "aaaImplement решение географически распределенных баз данных SQL Azure | Документы Microsoft"
description: "Узнайте, tooconfigure вашей базы данных SQL Azure и приложения для отработки отказа tooa репликации базы данных и тестовой отработки отказа."
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
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="41da8-103">Реализация географически распределенной базы данных</span><span class="sxs-lookup"><span data-stu-id="41da8-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="41da8-104">В этом учебнике Настройка базы данных Azure SQL и приложения для отработки отказа tooa удаленной области и затем протестируйте план, переход на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="41da8-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="41da8-105">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="41da8-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="41da8-106">создавать пользователей базы данных и предоставлять им разрешения;</span><span class="sxs-lookup"><span data-stu-id="41da8-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="41da8-107">настраивать правила брандмауэра уровня базы данных;</span><span class="sxs-lookup"><span data-stu-id="41da8-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="41da8-108">создавать [группу отработки отказа георепликации](sql-database-geo-replication-overview.md);</span><span class="sxs-lookup"><span data-stu-id="41da8-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="41da8-109">Создание и компиляция tooquery приложений Java из базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="41da8-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="41da8-110">выполнять отработку аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="41da8-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="41da8-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="41da8-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="41da8-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41da8-112">Prerequisites</span></span>

<span data-ttu-id="41da8-113">toocomplete завершения этого учебника, убедитесь, что hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="41da8-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="41da8-114">Последняя версия установленного hello [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="41da8-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="41da8-115">Установите базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41da8-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="41da8-116">В этом учебнике используется hello учебной базой данных AdventureWorksLT с именем **mySampleDatabase** из одного из этих краткие руководства:</span><span class="sxs-lookup"><span data-stu-id="41da8-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="41da8-117">Создание базы данных с помощью портала</span><span class="sxs-lookup"><span data-stu-id="41da8-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="41da8-118">Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="41da8-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="41da8-119">Создание базы данных с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="41da8-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="41da8-120">Определен метод tooexecute SQL скриптов к базе данных можно использовать один hello следующие средства:</span><span class="sxs-lookup"><span data-stu-id="41da8-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="41da8-121">редактор запросов Hello в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41da8-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="41da8-122">Дополнительные сведения об использовании редактора запросов hello в hello портала Azure см. в разделе [подключение и запрос, с помощью редактора запросов](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="41da8-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="41da8-123">Hello новейшую версию [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), который — это интегрированная среда для управления любой инфраструктуры SQL из SQL Server tooSQL базы данных для Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="41da8-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="41da8-124">Hello новейшую версию [кода Visual Studio](https://code.visualstudio.com/docs), являющийся редактором графический кода для Linux, macOS, и Windows, которые поддерживает расширения, включая hello [mssql расширения](https://aka.ms/mssql-marketplace) для выполнения запросов Microsoft SQL Server , База данных azure SQL и хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="41da8-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="41da8-125">Дополнительные сведения об использовании этого средства в базе данных SQL Azure см. в статье [База данных SQL Azure: подключение и запрос данных с помощью Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="41da8-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="41da8-126">Создание пользователей базы данных и предоставление им разрешений</span><span class="sxs-lookup"><span data-stu-id="41da8-126">Create database users and grant permissions</span></span>

<span data-ttu-id="41da8-127">Подключитесь tooyour базы данных и создайте учетные записи пользователей с помощью одного из hello следующие средства:</span><span class="sxs-lookup"><span data-stu-id="41da8-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="41da8-128">редактор запросов Hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="41da8-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="41da8-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="41da8-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="41da8-130">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="41da8-130">Visual Studio Code</span></span>

<span data-ttu-id="41da8-131">Эти учетные записи пользователей автоматически реплицировать tooyour сервера-получателя (и обеспечивать синхронизацию).</span><span class="sxs-lookup"><span data-stu-id="41da8-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="41da8-132">toouse SQL Server Management Studio или кода Visual Studio, может потребоваться tooconfigure правила брандмауэра при подключении клиента с IP-адресом, для которого вы еще не настроен брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="41da8-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="41da8-133">Подробные инструкции см. в разделе [Создание правила брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="41da8-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="41da8-134">В окне запроса выполните hello, выполнив запрос toocreate две учетные записи пользователя в базе данных.</span><span class="sxs-lookup"><span data-stu-id="41da8-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="41da8-135">Этот сценарий предоставляет **db_owner** toohello разрешений **app_admin** учетной записи и предоставляет **ВЫБЕРИТЕ** и **обновление** toohello разрешения **app_user** учетной записи.</span><span class="sxs-lookup"><span data-stu-id="41da8-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="41da8-136">Создание брандмауэра на уровне базы данных</span><span class="sxs-lookup"><span data-stu-id="41da8-136">Create database-level firewall</span></span>

<span data-ttu-id="41da8-137">Создайте [правило брандмауэра уровня базы данных](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="41da8-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="41da8-138">Это правило брандмауэра уровня базы данных автоматически реплицирует toohello сервера-получателя, созданный в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="41da8-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="41da8-139">Для простоты (в этом учебнике) Используйте общедоступный IP-адрес hello hello компьютера, на котором hello действия выполняются в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="41da8-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="41da8-140">toodetermine hello IP-адрес, используемый для hello правила брандмауэра уровня сервера для текущего компьютера, в разделе [создания брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="41da8-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="41da8-141">В окне Открыть запрос замените предыдущий запрос hello приветствия при следующем запросе, заменив hello IP-адресов hello соответствующие IP-адресов для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="41da8-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="41da8-142">Создание группы автоматической отработки отказа и активная георепликация</span><span class="sxs-lookup"><span data-stu-id="41da8-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="41da8-143">С помощью Azure PowerShell, создать [активной георепликации автоматического перехода на другой ресурс группы](sql-database-geo-replication-overview.md) между существующего сервера Azure SQL и hello новый пустой сервера Azure SQL в регионе Azure, а затем добавьте группе отработки отказа toohello образца базы данных.</span><span class="sxs-lookup"><span data-stu-id="41da8-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41da8-144">Для выполнения этих командлетов требуется Azure PowerShell версии 4.0.</span><span class="sxs-lookup"><span data-stu-id="41da8-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="41da8-145">Присвоения значений переменным для написания сценариев PowerShell, используя hello значения для существующего сервера и образец базы данных и предоставляют глобальное уникальное значение для имени группы перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="41da8-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

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

2. <span data-ttu-id="41da8-146">Создайте пустой резервный сервер в вашем регионе отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="41da8-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="41da8-147">Создайте группу отработки отказа между двумя серверами hello.</span><span class="sxs-lookup"><span data-stu-id="41da8-147">Create a failover group between hello two servers.</span></span>

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

4. <span data-ttu-id="41da8-148">Добавьте группу отказоустойчивого toohello вашей базы данных.</span><span class="sxs-lookup"><span data-stu-id="41da8-148">Add your database toohello failover group.</span></span>

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

## <a name="install-java-software"></a><span data-ttu-id="41da8-149">Установка программного обеспечения Java</span><span class="sxs-lookup"><span data-stu-id="41da8-149">Install Java software</span></span>

<span data-ttu-id="41da8-150">Hello в этом разделе предполагается, что представление о разработке с использованием Java и являются новый tooworking с базой данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="41da8-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="41da8-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="41da8-151">**Mac OS**</span></span>
<span data-ttu-id="41da8-152">Откройте терминала и перейдите в каталог tooa, куда планируется создание проекта Java.</span><span class="sxs-lookup"><span data-stu-id="41da8-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="41da8-153">Установка **brew** и **Maven** , введя hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="41da8-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="41da8-154">Подробные инструкции по установке и настройке среды Java и Maven go hello [построение приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)выберите **Java**выберите **MacOS**и следуйте Hello подробные инструкции по настройке шаг 1.2, 1.3 и Java и Maven.</span><span class="sxs-lookup"><span data-stu-id="41da8-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="41da8-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="41da8-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="41da8-156">Откройте терминала и перейдите в каталог tooa, куда планируется создание проекта Java.</span><span class="sxs-lookup"><span data-stu-id="41da8-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="41da8-157">Установка **Maven** , введя hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="41da8-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="41da8-158">Подробные инструкции по установке и настройке среды Java и Maven go hello [построение приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)выберите **Java**выберите **Ubuntu**и следуйте Hello подробные инструкции по настройке Java и Maven шаг 1.2, 1.3 и 1.4.</span><span class="sxs-lookup"><span data-stu-id="41da8-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="41da8-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="41da8-159">**Windows**</span></span>
<span data-ttu-id="41da8-160">Установка [Maven](https://maven.apache.org/download.cgi) с помощью установщика официальный hello.</span><span class="sxs-lookup"><span data-stu-id="41da8-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="41da8-161">Используйте Maven toohelp Управление зависимостями, создания, тестирования и запуска проекта Java.</span><span class="sxs-lookup"><span data-stu-id="41da8-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="41da8-162">Подробные инструкции по установке и настройке среды Java и Maven go hello [построение приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)выберите **Java**, выберите Windows, а затем следуйте hello подробные инструкции по Настройка Java и Maven на шаге 1.2 и 1.3.</span><span class="sxs-lookup"><span data-stu-id="41da8-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="41da8-163">Создание проекта SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="41da8-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="41da8-164">В командной консоли hello (таких как Bash) создайте проект Maven.</span><span class="sxs-lookup"><span data-stu-id="41da8-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="41da8-165">Введите **Y** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="41da8-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="41da8-166">Перейдите в только что созданный проект.</span><span class="sxs-lookup"><span data-stu-id="41da8-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="41da8-167">Используя текстовый редактор, откройте файл pom.xml hello в папку проекта.</span><span class="sxs-lookup"><span data-stu-id="41da8-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="41da8-168">Добавьте hello драйвера JDBC для SQL Server зависимостей tooyour Maven проекта, открыв в привычном текстовом редакторе и скопировав и вставив hello следующие строки в файл pom.xml.</span><span class="sxs-lookup"><span data-stu-id="41da8-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="41da8-169">Не перезаписывать существующие значения hello подставлена в файл hello.</span><span class="sxs-lookup"><span data-stu-id="41da8-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="41da8-170">Hello JDBC зависимостей необходимо вставить в () раздела hello большего «зависимости».</span><span class="sxs-lookup"><span data-stu-id="41da8-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="41da8-171">Укажите версию hello проект hello toocompile Java, для добавляя hello в следующем разделе «свойства» в файл pom.xml hello после раздела «зависимости» hello.</span><span class="sxs-lookup"><span data-stu-id="41da8-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="41da8-172">Добавьте следующие hello «сборки» раздел в файл pom.xml hello после hello раздел «свойства» toosupport манифеста файлов JAR-файлов.</span><span class="sxs-lookup"><span data-stu-id="41da8-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

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
8. <span data-ttu-id="41da8-173">Сохраните и закройте файл pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="41da8-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="41da8-174">Откройте файл App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) и замените содержимое hello hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="41da8-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="41da8-175">Замените имя группы отработки отказа hello hello имя для вашей группы перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="41da8-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="41da8-176">Если вы изменили значения hello hello имя базы данных, пользователя или пароль, измените эти значения также.</span><span class="sxs-lookup"><span data-stu-id="41da8-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

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
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
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
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
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
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
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
6. <span data-ttu-id="41da8-177">Сохраните и закройте файл App.java hello.</span><span class="sxs-lookup"><span data-stu-id="41da8-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="41da8-178">Компиляция и выполнение проекта SqlDbSample hello</span><span class="sxs-lookup"><span data-stu-id="41da8-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="41da8-179">В командной консоли hello выполните команду toofollowing.</span><span class="sxs-lookup"><span data-stu-id="41da8-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="41da8-180">После завершения выполнения hello, следующая команда toorun hello приложения (он выполняется для примерно 1 час, пока не будет остановлена пользователем вручную):</span><span class="sxs-lookup"><span data-stu-id="41da8-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="41da8-181">Выполнение отработки аварийного восстановления</span><span class="sxs-lookup"><span data-stu-id="41da8-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="41da8-182">Для группы отработки отказа вызовите отработку отказа вручную.</span><span class="sxs-lookup"><span data-stu-id="41da8-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="41da8-183">Наблюдать результаты приложения hello во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="41da8-183">Observe hello application results during failover.</span></span> <span data-ttu-id="41da8-184">Некоторые операции вставки ошибкой, пока обновит hello кэша DNS.</span><span class="sxs-lookup"><span data-stu-id="41da8-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="41da8-185">Узнайте, какую роль выполняет сервер аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="41da8-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="41da8-186">Восстановите размещение.</span><span class="sxs-lookup"><span data-stu-id="41da8-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="41da8-187">Наблюдать результаты приложения hello при отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="41da8-187">Observe hello application results during failback.</span></span> <span data-ttu-id="41da8-188">Некоторые операции вставки ошибкой, пока обновит hello кэша DNS.</span><span class="sxs-lookup"><span data-stu-id="41da8-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="41da8-189">Узнайте, какую роль выполняет сервер аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="41da8-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="41da8-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41da8-190">Next steps</span></span> 

<span data-ttu-id="41da8-191">Дополнительные сведения см. в статье [Обзор. Группы отработки отказа и активная георепликация](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="41da8-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
