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
# <a name="implement-a-geo-distributed-database"></a>Реализация географически распределенной базы данных

В этом учебнике Настройка базы данных Azure SQL и приложения для отработки отказа tooa удаленной области и затем протестируйте план, переход на другой ресурс. Вы узнаете, как выполнять следующие задачи: 

> [!div class="checklist"]
> * создавать пользователей базы данных и предоставлять им разрешения;
> * настраивать правила брандмауэра уровня базы данных;
> * создавать [группу отработки отказа георепликации](sql-database-geo-replication-overview.md);
> * Создание и компиляция tooquery приложений Java из базы данных Azure SQL
> * выполнять отработку аварийного восстановления.

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.


## <a name="prerequisites"></a>Предварительные требования

toocomplete завершения этого учебника, убедитесь, что hello следующие предварительные требования:

- Последняя версия установленного hello [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Установите базу данных SQL Azure. В этом учебнике используется hello учебной базой данных AdventureWorksLT с именем **mySampleDatabase** из одного из этих краткие руководства:

   - [Создание базы данных с помощью портала](sql-database-get-started-portal.md)
   - [Создание базы данных SQL Azure и отправка к ней запросов с помощью Azure CLI](sql-database-get-started-cli.md)
   - [Создание базы данных с помощью PowerShell](sql-database-get-started-powershell.md)

- Определен метод tooexecute SQL скриптов к базе данных можно использовать один hello следующие средства:
   - редактор запросов Hello в hello [портал Azure](https://portal.azure.com). Дополнительные сведения об использовании редактора запросов hello в hello портала Azure см. в разделе [подключение и запрос, с помощью редактора запросов](sql-database-get-started-portal.md#query-the-sql-database).
   - Hello новейшую версию [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), который — это интегрированная среда для управления любой инфраструктуры SQL из SQL Server tooSQL базы данных для Microsoft Windows.
   - Hello новейшую версию [кода Visual Studio](https://code.visualstudio.com/docs), являющийся редактором графический кода для Linux, macOS, и Windows, которые поддерживает расширения, включая hello [mssql расширения](https://aka.ms/mssql-marketplace) для выполнения запросов Microsoft SQL Server , База данных azure SQL и хранилище данных SQL. Дополнительные сведения об использовании этого средства в базе данных SQL Azure см. в статье [База данных SQL Azure: подключение и запрос данных с помощью Visual Studio Code](sql-database-connect-query-vscode.md). 

## <a name="create-database-users-and-grant-permissions"></a>Создание пользователей базы данных и предоставление им разрешений

Подключитесь tooyour базы данных и создайте учетные записи пользователей с помощью одного из hello следующие средства:

- редактор запросов Hello в hello портал Azure
- SQL Server Management Studio
- Visual Studio Code.

Эти учетные записи пользователей автоматически реплицировать tooyour сервера-получателя (и обеспечивать синхронизацию). toouse SQL Server Management Studio или кода Visual Studio, может потребоваться tooconfigure правила брандмауэра при подключении клиента с IP-адресом, для которого вы еще не настроен брандмауэр. Подробные инструкции см. в разделе [Создание правила брандмауэра на уровне сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).

- В окне запроса выполните hello, выполнив запрос toocreate две учетные записи пользователя в базе данных. Этот сценарий предоставляет **db_owner** toohello разрешений **app_admin** учетной записи и предоставляет **ВЫБЕРИТЕ** и **обновление** toohello разрешения **app_user** учетной записи. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Создание брандмауэра на уровне базы данных

Создайте [правило брандмауэра уровня базы данных](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) для базы данных SQL. Это правило брандмауэра уровня базы данных автоматически реплицирует toohello сервера-получателя, созданный в этом учебнике. Для простоты (в этом учебнике) Используйте общедоступный IP-адрес hello hello компьютера, на котором hello действия выполняются в этом учебнике. toodetermine hello IP-адрес, используемый для hello правила брандмауэра уровня сервера для текущего компьютера, в разделе [создания брандмауэра уровня сервера](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- В окне Открыть запрос замените предыдущий запрос hello приветствия при следующем запросе, заменив hello IP-адресов hello соответствующие IP-адресов для вашей среды.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Создание группы автоматической отработки отказа и активная георепликация 

С помощью Azure PowerShell, создать [активной георепликации автоматического перехода на другой ресурс группы](sql-database-geo-replication-overview.md) между существующего сервера Azure SQL и hello новый пустой сервера Azure SQL в регионе Azure, а затем добавьте группе отработки отказа toohello образца базы данных.

> [!IMPORTANT]
> Для выполнения этих командлетов требуется Azure PowerShell версии 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Присвоения значений переменным для написания сценариев PowerShell, используя hello значения для существующего сервера и образец базы данных и предоставляют глобальное уникальное значение для имени группы перехода на другой ресурс.

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

2. Создайте пустой резервный сервер в вашем регионе отработки отказа.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Создайте группу отработки отказа между двумя серверами hello.

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

4. Добавьте группу отказоустойчивого toohello вашей базы данных.

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

## <a name="install-java-software"></a>Установка программного обеспечения Java

Hello в этом разделе предполагается, что представление о разработке с использованием Java и являются новый tooworking с базой данных SQL Azure. 

### <a name="mac-os"></a>**Mac OS**
Откройте терминала и перейдите в каталог tooa, куда планируется создание проекта Java. Установка **brew** и **Maven** , введя hello, следующие команды: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Подробные инструкции по установке и настройке среды Java и Maven go hello [построение приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)выберите **Java**выберите **MacOS**и следуйте Hello подробные инструкции по настройке шаг 1.2, 1.3 и Java и Maven.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Откройте терминала и перейдите в каталог tooa, куда планируется создание проекта Java. Установка **Maven** , введя hello, следующие команды:

```bash
sudo apt-get install maven
```

Подробные инструкции по установке и настройке среды Java и Maven go hello [построение приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)выберите **Java**выберите **Ubuntu**и следуйте Hello подробные инструкции по настройке Java и Maven шаг 1.2, 1.3 и 1.4.

### <a name="windows"></a>**Windows**
Установка [Maven](https://maven.apache.org/download.cgi) с помощью установщика официальный hello. Используйте Maven toohelp Управление зависимостями, создания, тестирования и запуска проекта Java. Подробные инструкции по установке и настройке среды Java и Maven go hello [построение приложения с помощью SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)выберите **Java**, выберите Windows, а затем следуйте hello подробные инструкции по Настройка Java и Maven на шаге 1.2 и 1.3.

## <a name="create-sqldbsample-project"></a>Создание проекта SqlDbSample

1. В командной консоли hello (таких как Bash) создайте проект Maven. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Введите **Y** и нажмите клавишу **ВВОД**.
3. Перейдите в только что созданный проект.

   ```bash
   cd SqlDbSamples
   ```

4. Используя текстовый редактор, откройте файл pom.xml hello в папку проекта. 

5. Добавьте hello драйвера JDBC для SQL Server зависимостей tooyour Maven проекта, открыв в привычном текстовом редакторе и скопировав и вставив hello следующие строки в файл pom.xml. Не перезаписывать существующие значения hello подставлена в файл hello. Hello JDBC зависимостей необходимо вставить в () раздела hello большего «зависимости».   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Укажите версию hello проект hello toocompile Java, для добавляя hello в следующем разделе «свойства» в файл pom.xml hello после раздела «зависимости» hello. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Добавьте следующие hello «сборки» раздел в файл pom.xml hello после hello раздел «свойства» toosupport манифеста файлов JAR-файлов.       

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
8. Сохраните и закройте файл pom.xml hello.
9. Откройте файл App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) и замените содержимое hello hello после содержимого. Замените имя группы отработки отказа hello hello имя для вашей группы перехода на другой ресурс. Если вы изменили значения hello hello имя базы данных, пользователя или пароль, измените эти значения также.

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
6. Сохраните и закройте файл App.java hello.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Компиляция и выполнение проекта SqlDbSample hello

1. В командной консоли hello выполните команду toofollowing.

   ```bash
   mvn package
   ```
2. После завершения выполнения hello, следующая команда toorun hello приложения (он выполняется для примерно 1 час, пока не будет остановлена пользователем вручную):

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Выполнение отработки аварийного восстановления

1. Для группы отработки отказа вызовите отработку отказа вручную. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Наблюдать результаты приложения hello во время отработки отказа. Некоторые операции вставки ошибкой, пока обновит hello кэша DNS.     

3. Узнайте, какую роль выполняет сервер аварийного восстановления.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Восстановите размещение.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Наблюдать результаты приложения hello при отработке отказа. Некоторые операции вставки ошибкой, пока обновит hello кэша DNS.     

6. Узнайте, какую роль выполняет сервер аварийного восстановления.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Дальнейшие действия 

Дополнительные сведения см. в статье [Обзор. Группы отработки отказа и активная георепликация](sql-database-geo-replication-overview.md).
