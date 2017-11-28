---
title: "aaaImplement многопользовательского приложения SaaS с базой данных SQL Azure | Документы Microsoft"
description: "Реализация мультитенантного приложения SaaS с помощью базы данных SQL Azure."
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="b49e3-103">Реализация мультитенантного приложения SaaS с помощью базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b49e3-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="b49e3-104">Многопользовательское приложение — это приложение, размещенных в облачной среде и предоставляющий hello же набор служб toohundreds или тысяч клиентов, которые не используют и не отображаются данные друг друга.</span><span class="sxs-lookup"><span data-stu-id="b49e3-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="b49e3-105">Примером является приложение SaaS, которое обеспечивает tootenants службы в среде, размещаемых в облаке.</span><span class="sxs-lookup"><span data-stu-id="b49e3-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="b49e3-106">Эта модель изолирует hello данных для каждого клиента и оптимизирует hello распределение ресурсов для затрат.</span><span class="sxs-lookup"><span data-stu-id="b49e3-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="b49e3-107">В этом учебнике показано как toocreate многопользовательского приложения SaaS, с помощью базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b49e3-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="b49e3-108">Из этого руководства вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="b49e3-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b49e3-109">Настройка базы данных среды toosupport многопользовательскому приложению SaaS, с помощью шаблона базы данных каждого клиента hello</span><span class="sxs-lookup"><span data-stu-id="b49e3-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="b49e3-110">Как создать каталог клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="b49e3-111">Подготовка базы данных клиента и зарегистрировать его в каталоге клиента hello</span><span class="sxs-lookup"><span data-stu-id="b49e3-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="b49e3-112">Как настроить пример приложения Java.</span><span class="sxs-lookup"><span data-stu-id="b49e3-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="b49e3-113">Как получить доступ к клиентским базам данных через простое консольное приложение Java.</span><span class="sxs-lookup"><span data-stu-id="b49e3-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="b49e3-114">Как удалить клиент.</span><span class="sxs-lookup"><span data-stu-id="b49e3-114">Delete a tenant</span></span>

<span data-ttu-id="b49e3-115">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="b49e3-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b49e3-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b49e3-116">Prerequisites</span></span>

<span data-ttu-id="b49e3-117">toocomplete этого учебника, убедитесь в наличии:</span><span class="sxs-lookup"><span data-stu-id="b49e3-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="b49e3-118">Последнюю версию установленного hello hello и PowerShell [последнего выпуска пакета SDK Azure PowerShell](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b49e3-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="b49e3-119">Установленные hello последнюю версию [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="b49e3-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="b49e3-120">Установка SQL Server Management Studio также включает последнюю версию hello SQLPackage, программы командной строки, которое может быть используется tooautomate задачи разработки базы данных.</span><span class="sxs-lookup"><span data-stu-id="b49e3-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="b49e3-121">Установленные hello [среда выполнения Java (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) и hello [последние JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b49e3-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="b49e3-122">[Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="b49e3-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="b49e3-123">Будет использоваться maven toohelp Управление зависимостями, создания, тестирования и запуска проекта Java образец hello</span><span class="sxs-lookup"><span data-stu-id="b49e3-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="b49e3-124">Настройка среды данных</span><span class="sxs-lookup"><span data-stu-id="b49e3-124">Set up data environment</span></span>

<span data-ttu-id="b49e3-125">Вам необходимо подготовить базу данных для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="b49e3-126">модель базы данных каждого клиента Hello обеспечивает наивысшую степень изоляции между клиентами и низкие затраты на DevOps hello.</span><span class="sxs-lookup"><span data-stu-id="b49e3-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="b49e3-127">стоимость hello toooptimize облачных ресурсов, будут также ли администраторы базы данных клиента hello в пуле эластичных БД, позволяющий toooptimize hello цены производительности для группы баз данных.</span><span class="sxs-lookup"><span data-stu-id="b49e3-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="b49e3-128">toolearn о другой базе данных, подготовки моделей [см. Здесь](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="b49e3-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="b49e3-129">Выполните эти шаги toocreate SQL server и эластичного пула, в котором будет размещаться всех баз данных клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="b49e3-130">Создайте переменные toostore значения, которые будут использоваться hello конца hello учебника.</span><span class="sxs-lookup"><span data-stu-id="b49e3-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="b49e3-131">Убедитесь, что toomodify hello IP адрес переменной tooinclude IP-адреса</span><span class="sxs-lookup"><span data-stu-id="b49e3-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="b49e3-132">TooAzure входа и создать пул SQL server и переменной ширины</span><span class="sxs-lookup"><span data-stu-id="b49e3-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="b49e3-133">Создание каталога клиента</span><span class="sxs-lookup"><span data-stu-id="b49e3-133">Create tenant catalog</span></span> 

<span data-ttu-id="b49e3-134">В приложении SaaS несколькими клиентами это важные tooknow, в котором хранятся сведения для клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="b49e3-135">Обычно они хранятся в базе данных каталога.</span><span class="sxs-lookup"><span data-stu-id="b49e3-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="b49e3-136">База данных каталога Hello является toohold используется сопоставление между клиентом и базы данных, в которой хранятся данные этого клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="b49e3-137">базовый шаблон Hello применяет ли многопользовательское или использования базы данных одного клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="b49e3-138">Выполните эти шаги toocreate база данных каталога для приложения SaaS образец hello.</span><span class="sxs-lookup"><span data-stu-id="b49e3-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="b49e3-139">Подготовка базы данных для клиента tenant1 и его регистрация в клиентском каталоге</span><span class="sxs-lookup"><span data-stu-id="b49e3-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="b49e3-140">Используйте Powershell tooprovision базы данных для нового клиента «клиента (1)» и регистрация этого клиента в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="b49e3-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="b49e3-141">Подготовка базы данных для клиента tenant2 и его регистрация в клиентском каталоге</span><span class="sxs-lookup"><span data-stu-id="b49e3-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="b49e3-142">Используйте Powershell tooprovision базы данных для нового клиента «tenant2» и регистрация этого клиента в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="b49e3-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in hello tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="b49e3-143">Настройка примера приложения Java</span><span class="sxs-lookup"><span data-stu-id="b49e3-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="b49e3-144">Создайте проект Maven.</span><span class="sxs-lookup"><span data-stu-id="b49e3-144">Create a maven project.</span></span> <span data-ttu-id="b49e3-145">Введите ниже hello в окне командной строки:</span><span class="sxs-lookup"><span data-stu-id="b49e3-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="b49e3-146">Добавьте этот зависимостей, уровне языка и построения параметр toosupport файлы манифеста в файле pom.xml toohello JAR-файлов:</span><span class="sxs-lookup"><span data-stu-id="b49e3-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. <span data-ttu-id="b49e3-147">Добавьте следующий текст hello в файл App.java hello:</span><span class="sxs-lookup"><span data-stu-id="b49e3-147">Add hello following into hello App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in hello system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="b49e3-148">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="b49e3-148">Save hello file.</span></span>

5. <span data-ttu-id="b49e3-149">Перейдите в консоли toocommand и выполнение</span><span class="sxs-lookup"><span data-stu-id="b49e3-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="b49e3-150">После завершения выполнения следующие приложения hello toorun hello</span><span class="sxs-lookup"><span data-stu-id="b49e3-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="b49e3-151">в случае успешного выполнения, Hello выходных данных будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b49e3-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="b49e3-152">Удаление первого клиента</span><span class="sxs-lookup"><span data-stu-id="b49e3-152">Delete first tenant</span></span> 
<span data-ttu-id="b49e3-153">Используйте PowerShell toodelete hello клиента базы данных и каталога записи для первого клиента hello.</span><span class="sxs-lookup"><span data-stu-id="b49e3-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="b49e3-154">Попробуйте подключиться слишком Здравствуйте приложения Java, с помощью клиента «(1)».</span><span class="sxs-lookup"><span data-stu-id="b49e3-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="b49e3-155">Вы получите сообщение о том, что этому клиенту hello не существует.</span><span class="sxs-lookup"><span data-stu-id="b49e3-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b49e3-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b49e3-156">Next steps</span></span> 

<span data-ttu-id="b49e3-157">Из этого руководства вы узнали следующее:</span><span class="sxs-lookup"><span data-stu-id="b49e3-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b49e3-158">Настройка базы данных среды toosupport многопользовательскому приложению SaaS, с помощью шаблона базы данных каждого клиента hello</span><span class="sxs-lookup"><span data-stu-id="b49e3-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="b49e3-159">Как создать каталог клиента.</span><span class="sxs-lookup"><span data-stu-id="b49e3-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="b49e3-160">Подготовка базы данных клиента и зарегистрировать его в каталоге клиента hello</span><span class="sxs-lookup"><span data-stu-id="b49e3-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="b49e3-161">Как настроить пример приложения Java.</span><span class="sxs-lookup"><span data-stu-id="b49e3-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="b49e3-162">Как получить доступ к клиентским базам данных через простое консольное приложение Java.</span><span class="sxs-lookup"><span data-stu-id="b49e3-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="b49e3-163">Как удалить клиент.</span><span class="sxs-lookup"><span data-stu-id="b49e3-163">Delete a tenant</span></span>

* <span data-ttu-id="b49e3-164">Примеры PowerShell для выполнения стандартных задач см. в статье [Примеры Azure PowerShell для базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples).</span><span class="sxs-lookup"><span data-stu-id="b49e3-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="b49e3-165">Дополнительные сведения о шаблонах разработки для мультитенантных приложений SaaS и базы данных SQL Azure см. в [этой статье](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications).</span><span class="sxs-lookup"><span data-stu-id="b49e3-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="b49e3-166">Примеры Java для стандартных задач Azure см. в [центре разработчиков Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="b49e3-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



