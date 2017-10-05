---
title: "Реализация мультитенантного приложения SaaS с помощью базы данных SQL Azure | Документация Майкрософт"
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
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="1b796-103">Реализация мультитенантного приложения SaaS с помощью базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1b796-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="1b796-104">Мультитенатное приложение — это приложение, расположенное в облачной среде и предоставляющее одинаковый набор служб сотням или тысячам клиентов, которые не используют данные совместно и не обращаются к данным друг друга.</span><span class="sxs-lookup"><span data-stu-id="1b796-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="1b796-105">В качестве примера можно привести приложение SaaS, которое предоставляет службы для клиентов в размещенной в облаке среде.</span><span class="sxs-lookup"><span data-stu-id="1b796-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="1b796-106">Эта модель изолирует данные для каждого клиента и улучшает распределение ресурсов для оптимизации затрат.</span><span class="sxs-lookup"><span data-stu-id="1b796-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="1b796-107">В этом руководстве рассматривается создание мультитенантного приложения SaaS с помощью базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1b796-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="1b796-108">Из этого руководства вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="1b796-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1b796-109">Как настроить среду базы данных для поддержки мультитенантного приложения SaaS с помощью шаблона базы данных на клиент.</span><span class="sxs-lookup"><span data-stu-id="1b796-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="1b796-110">Как создать каталог клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="1b796-111">Как подготовить клиентскую базу данных и зарегистрировать ее в каталоге клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="1b796-112">Как настроить пример приложения Java.</span><span class="sxs-lookup"><span data-stu-id="1b796-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="1b796-113">Как получить доступ к клиентским базам данных через простое консольное приложение Java.</span><span class="sxs-lookup"><span data-stu-id="1b796-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="1b796-114">Как удалить клиент.</span><span class="sxs-lookup"><span data-stu-id="1b796-114">Delete a tenant</span></span>

<span data-ttu-id="1b796-115">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="1b796-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b796-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b796-116">Prerequisites</span></span>

<span data-ttu-id="1b796-117">В рамках этого руководства вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="1b796-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="1b796-118">Последняя версия PowerShell и [последний выпуск пакета SDK для Azure PowerShell](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1b796-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="1b796-119">Последняя версия [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="1b796-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="1b796-120">При установке SQL Server Management Studio также устанавливается последняя версия SqlPackage, служебной программы командной строки, которую можно использовать для автоматизации ряда задач по разработке базы данных.</span><span class="sxs-lookup"><span data-stu-id="1b796-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="1b796-121">[Среда выполнения Java (JRE) версии 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) и [последний пакет JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="1b796-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="1b796-122">[Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="1b796-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="1b796-123">Maven можно использовать для управления зависимостями, сборки, тестирования и запуска примера проекта Java.</span><span class="sxs-lookup"><span data-stu-id="1b796-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="1b796-124">Настройка среды данных</span><span class="sxs-lookup"><span data-stu-id="1b796-124">Set up data environment</span></span>

<span data-ttu-id="1b796-125">Вам необходимо подготовить базу данных для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="1b796-126">Модель "база данных на клиент" обеспечивает максимальный уровень изоляции между клиентами и небольшую стоимость разработки и выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="1b796-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="1b796-127">Чтобы оптимизировать стоимость облачных ресурсов, вам также необходимо подготовить клиентские базы данных для размещения в эластичном пуле, что позволит оптимизировать соотношение цены и производительности для группы баз данных.</span><span class="sxs-lookup"><span data-stu-id="1b796-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="1b796-128">Дополнительные сведения о других моделях подготовки базы данных см. в разделе [Модели данных мультитенантного приложения](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="1b796-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="1b796-129">Следуйте инструкциям ниже, чтобы создать SQL Server и эластичный пул для размещения всех клиентских баз данных.</span><span class="sxs-lookup"><span data-stu-id="1b796-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="1b796-130">Создайте переменные для хранения значений, которые будут использоваться дальше.</span><span class="sxs-lookup"><span data-stu-id="1b796-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="1b796-131">Измените переменную IP-адреса, добавив свой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="1b796-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="1b796-132">Войдите в Azure и создайте SQL Server и эластичный пул.</span><span class="sxs-lookup"><span data-stu-id="1b796-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="1b796-133">Создание каталога клиента</span><span class="sxs-lookup"><span data-stu-id="1b796-133">Create tenant catalog</span></span> 

<span data-ttu-id="1b796-134">В мультитенантном приложении SaaS важно знать, где хранятся сведения для клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="1b796-135">Обычно они хранятся в базе данных каталога.</span><span class="sxs-lookup"><span data-stu-id="1b796-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="1b796-136">База данных каталога используется для хранения сопоставления между клиентом и базой данных, в которой хранятся данные клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="1b796-137">Независимо от того, как база данных используется (мультитенантная или с одним клиентом), применяется основной шаблон.</span><span class="sxs-lookup"><span data-stu-id="1b796-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="1b796-138">Выполните приведенные ниже инструкции, чтобы создать базу данных каталога для примера приложения SaaS.</span><span class="sxs-lookup"><span data-stu-id="1b796-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="1b796-139">Подготовка базы данных для клиента tenant1 и его регистрация в клиентском каталоге</span><span class="sxs-lookup"><span data-stu-id="1b796-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="1b796-140">Используйте Powershell, чтобы подготовить базу данных для нового клиента tenant1 и зарегистрировать его в каталоге.</span><span class="sxs-lookup"><span data-stu-id="1b796-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
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

# Register 'tenant1' in the tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="1b796-141">Подготовка базы данных для клиента tenant2 и его регистрация в клиентском каталоге</span><span class="sxs-lookup"><span data-stu-id="1b796-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="1b796-142">Используйте Powershell, чтобы подготовить базу данных для нового клиента tenant2 и зарегистрировать его в каталоге.</span><span class="sxs-lookup"><span data-stu-id="1b796-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
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

# Register tenant 'tenant2' in the tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="1b796-143">Настройка примера приложения Java</span><span class="sxs-lookup"><span data-stu-id="1b796-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="1b796-144">Создайте проект Maven.</span><span class="sxs-lookup"><span data-stu-id="1b796-144">Create a maven project.</span></span> <span data-ttu-id="1b796-145">В окне командной строки введите следующее:</span><span class="sxs-lookup"><span data-stu-id="1b796-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="1b796-146">Добавьте зависимость, уровень языка и параметр сборки для поддержки файлов манифестов в JAR в файл pom.xml:</span><span class="sxs-lookup"><span data-stu-id="1b796-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
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

3. <span data-ttu-id="1b796-147">В файл App.java добавьте следующее:</span><span class="sxs-lookup"><span data-stu-id="1b796-147">Add the following into the App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
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
   
   // List all tenants that currently exist in the system
   
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
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
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

4. <span data-ttu-id="1b796-148">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="1b796-148">Save the file.</span></span>

5. <span data-ttu-id="1b796-149">Перейдите в командную консоль и выполните команду ниже.</span><span class="sxs-lookup"><span data-stu-id="1b796-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="1b796-150">После ее завершения выполните следующую команду, чтобы запустить приложение:</span><span class="sxs-lookup"><span data-stu-id="1b796-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="1b796-151">В случае успешного запуска выходные данные будут выглядеть примерно следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1b796-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="1b796-152">Удаление первого клиента</span><span class="sxs-lookup"><span data-stu-id="1b796-152">Delete first tenant</span></span> 
<span data-ttu-id="1b796-153">Используйте PowerShell, чтобы удалить клиентскую базу данных и запись каталога для первого клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

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

<span data-ttu-id="1b796-154">Попробуйте подключиться к клиенту tenant1 с помощью приложения Java.</span><span class="sxs-lookup"><span data-stu-id="1b796-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="1b796-155">Вы получите ошибку с сообщением о том, что клиент не существует.</span><span class="sxs-lookup"><span data-stu-id="1b796-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b796-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b796-156">Next steps</span></span> 

<span data-ttu-id="1b796-157">Из этого руководства вы узнали следующее:</span><span class="sxs-lookup"><span data-stu-id="1b796-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1b796-158">Как настроить среду базы данных для поддержки мультитенантного приложения SaaS с помощью шаблона базы данных на клиент.</span><span class="sxs-lookup"><span data-stu-id="1b796-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="1b796-159">Как создать каталог клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="1b796-160">Как подготовить клиентскую базу данных и зарегистрировать ее в каталоге клиента.</span><span class="sxs-lookup"><span data-stu-id="1b796-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="1b796-161">Как настроить пример приложения Java.</span><span class="sxs-lookup"><span data-stu-id="1b796-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="1b796-162">Как получить доступ к клиентским базам данных через простое консольное приложение Java.</span><span class="sxs-lookup"><span data-stu-id="1b796-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="1b796-163">Как удалить клиент.</span><span class="sxs-lookup"><span data-stu-id="1b796-163">Delete a tenant</span></span>

* <span data-ttu-id="1b796-164">Примеры PowerShell для выполнения стандартных задач см. в статье [Примеры Azure PowerShell для базы данных SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples).</span><span class="sxs-lookup"><span data-stu-id="1b796-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="1b796-165">Дополнительные сведения о шаблонах разработки для мультитенантных приложений SaaS и базы данных SQL Azure см. в [этой статье](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications).</span><span class="sxs-lookup"><span data-stu-id="1b796-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="1b796-166">Примеры Java для стандартных задач Azure см. в [центре разработчиков Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="1b796-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



