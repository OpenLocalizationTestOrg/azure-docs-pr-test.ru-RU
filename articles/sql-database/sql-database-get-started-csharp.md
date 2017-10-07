---
title: "C#: начало работы с базой данных SQL Azure | Документация Майкрософт"
description: "Выберите базу данных SQL для разработки приложений SQL и C# и создания базы данных SQL Azure с помощью C# с помощью hello библиотеки базы данных SQL для .NET."
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
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>Используйте C# toocreate базы данных SQL с hello библиотеки базы данных SQL для .NET

Узнайте, как базы данных toocreate toouse C# Azure SQL с hello [Библиотека управления SQL Microsoft Azure для .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). В этой статье описывается, как toocreate одной базы данных SQL и C#. эластичные пулы toocreate, в разделе [создать эластичный пул](sql-database-elastic-pool-manage-csharp.md).

Hello Библиотека управления базы данных SQL Azure для .NET предоставляет [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md)-на основе API, который создает оболочку для hello [диспетчер ресурсов на основе REST API базы данных SQL](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Множество новых функций базы данных SQL поддерживаются только в том случае, если вы используете hello [модели развертывания диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md), поэтому следует всегда использовать hello последней **Библиотека управления базы данных SQL Azure для .NET ([документы](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [пакет NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. более старые Hello [классической модели развертывания на основе библиотеки](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) поддерживаются только в целях обратной совместимости, поэтому мы рекомендуем использовать диспетчер ресурсов на основе библиотеки более новой версии hello.
> 
> 

в этой статье инструкциям toocomplete hello, необходимо hello следующее:

* Подписка Azure. Если необходимо получить подписку Azure, просто щелкните **БЕСПЛАТНУЮ учетную запись** вверху hello это страница, а затем вернуться toofinish в этой статье.
* приведенному. Бесплатную копию Visual Studio, в разделе hello [загрузки Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) страницы.

> [!NOTE]
> В этой статье рассматривается создание пустой базы данных SQL. Изменение hello *CreateOrUpdateDatabase(...)*  метод в следующих образцов баз данных toocopy hello, масштабирование баз данных, создать базу данных в пул, и т. д.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Создайте консольное приложение и установите hello необходимые библиотеки
1. Запустите Visual Studio.
2. Выберите **Файл** > **Создать** > **Проект**.
3. Создайте на языке C# **консольное приложение** и присвойте ему имя *SqlDbConsoleApp*

toocreate базы данных SQL с помощью C#, hello нагрузки необходимых библиотек управления (с помощью hello [консоли диспетчера пакетов](http://docs.nuget.org/Consume/Package-Manager-Console)):

1. Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.
2. Тип `Install-Package Microsoft.Azure.Management.Sql -Pre` последние hello tooinstall [библиотеки управления Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Тип `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [библиотеки диспетчера ресурсов Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Тип `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [общая библиотека проверки подлинности Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Hello примеры в этой статье с помощью синхронного формы каждого запроса API и блок до завершения вызова REST hello на hello соответствующая служба. Доступны асинхронные методы.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Создание сервера базы данных SQL, правила брандмауэра и базы данных SQL — пример на языке C#
Следующий образец Hello создает группу ресурсов, сервера, правила брандмауэра и базы данных SQL. В разделе, [создать ресурсы tooaccess участника службы](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` переменных.

Замените содержимое hello **Program.cs** следующие hello и обновление hello `{variables}` значениями вашего приложения (не включайте hello `{}`).

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

        // Create management clients for hello Azure resources your app needs toowork with.
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


            Console.WriteLine("Press any key toocontinue...");
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
            // Retrieve hello server that will host this database
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





## <a name="create-a-service-principal-tooaccess-resources"></a>Создать tooaccess участника службы, ресурсы
Hello следующий сценарий PowerShell создает приложение hello Active Directory (AD) и службу hello основной, что нам потребуется tooauthenticate нашего приложения C#. сценарий Hello генерирует значения, которые мы должны hello, предшествующий C# образцы. Дополнительные сведения см. в разделе [toocreate использование Azure PowerShell участника службы ресурсов tooaccess](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы пытались базы данных SQL и настройка базы данных с помощью C#, вы будете готовы для hello в следующих статьях:

* [Подключать tooSQL базы данных SQL Server Management Studio и выполнить пробный запрос T-SQL](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Дополнительные ресурсы
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
