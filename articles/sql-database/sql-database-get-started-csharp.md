---
title: "C#: начало работы с базой данных SQL Azure | Документация Майкрософт"
description: "Используйте базы данных SQL для разработки приложений на основе SQL и C#. Создайте базу данных Azure SQL с помощью C# и библиотеки баз данных SQL для .NET."
keywords: "использование sql, sql и c#"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: c8a2703da1ee3687f8d134e768dd8d31dc4f316b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-c-to-create-a-sql-database-with-the-sql-database-library-for-net"></a>Создание базы данных SQL с помощью C# и библиотеки базы данных SQL для .NET

Узнайте, как использовать язык C# для создания базы данных SQL Azure с помощью [библиотеки управления базами данных SQL Microsoft Azure для .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). В этой статье описываются способы создания отдельной базы данных с помощью SQL и C#. Создание эластичных пулов описано в статье [Создание пула эластичных баз данных с помощью C#](sql-database-elastic-pool-manage-csharp.md).

Библиотека управления базами данных SQL Azure для .NET предоставляет API на основе [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), который служит оболочкой для [REST API базы данных SQL на основе Resource Manager](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Многие новые функции базы данных SQL поддерживаются только при использовании [модели развертывания с помощью Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). Поэтому всегда используйте последнюю **библиотеку управления базами данных SQL Azure для .NET ([документы](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [пакет NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Более ранние [библиотеки на основе классической модели развертывания](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) поддерживаются только для обратной совместимости. Поэтому советуем использовать более новые библиотеки на основе Resource Manager.
> 
> 

Чтобы выполнить действия, описанные в этой статье, необходимо следующее:

* Подписка Azure. Если вам требуется подписка Azure, нажмите в верхней части этой страницы кнопку **Бесплатная учетная запись**. Оформив подписку, вернитесь к этой статье.
* приведенному. Бесплатный экземпляр Visual Studio см. на странице [Скачиваемые файлы для Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs).

> [!NOTE]
> В этой статье рассматривается создание пустой базы данных SQL. В примере ниже измените метод *CreateOrUpdateDatabase(...)*, чтобы создать базу данных в пуле, копировать и масштабировать ее и т. д.  
> 

## <a name="create-a-console-app-and-install-the-required-libraries"></a>Создание консольного приложения и установка необходимых библиотек
1. Запустите Visual Studio.
2. Выберите **Файл** > **Создать** > **Проект**.
3. Создайте на языке C# **консольное приложение** и присвойте ему имя *SqlDbConsoleApp*

Чтобы создать базу данных SQL с помощью C#, загрузите необходимые библиотеки управления (используя [консоль диспетчера пакетов](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.
2. Введите `Install-Package Microsoft.Azure.Management.Sql -Pre`, чтобы установить последнюю [библиотеку управления SQL Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Введите `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` , чтобы установить [библиотеку управления Microsoft Azure Resource Manager](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Введите `Install-Package Microsoft.Azure.Common.Authentication -Pre` , чтобы установить [библиотеку управления общей проверки подлинности Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Примеры в этой статье используют синхронную форму каждого запроса API и блокируют до завершения вызова REST на базовой службе. Доступны асинхронные методы.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Создание сервера базы данных SQL, правила брандмауэра и базы данных SQL — пример на языке C#
В следующем примере создается группа ресурсов, сервер, правило брандмауэра и база данных SQL. Чтобы получить переменные `_subscriptionId, _tenantId, _applicationId, and _applicationSecret`, см. раздел [Создание субъекта-службы для доступа к ресурсам](#create-a-service-principal-to-access-resources).

Замените содержимое файла **Program.cs** приведенным ниже кодом и обновите `{variables}`, используя значения для своего приложения (удалите `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for the Azure resources your app needs to work with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key to continue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve the server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-to-access-resources"></a>Создание субъекта-службы для доступа к ресурсам
Следующий сценарий PowerShell создает приложение Active Directory (AD) и субъект-службу, которые необходимы для проверки подлинности нашего приложения C#. Сценарий выводит значения, необходимые для предыдущего примера на C#. Дополнительные сведения см. в статье [Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in to Azure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set to the subscription you want to work with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is the display name for your app, must be unique in your directory.
    # $uri does not need to be a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for the app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # To avoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun the following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output the values we need for our C# application to successfully authenticate

    Write-Output "Copy these values into the C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Дальнейшие действия
Вы уже познакомились с базами данных SQL и настроили базу данных с помощью C#. Теперь можно перейти к изучению следующих статей.

* [Подключение к базе данных SQL с помощью SQL Server Management Studio и выполнение пробного запроса T-SQL](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>дополнительные ресурсы.
* [База данных SQL](https://azure.microsoft.com/documentation/services/sql-database/)
* [Database Class (Класс базы данных)](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
