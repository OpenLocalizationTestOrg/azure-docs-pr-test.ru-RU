---
title: "Управление кластерами Hadoop в HDInsight с помощью пакета SDK для .NET — Azure | Документация Майкрософт"
description: "Узнайте, как осуществлять управление кластерами Hadoop в HDInsight с помощью пакета SDK для HDInsight .NET."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2017
ms.author: jgao
ms.openlocfilehash: d881d47e26460d3fff89c01245bba4c608dc8b08
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Управление кластерами Hadoop в HDInsight с помощью пакета SDK для .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Научитесь управлять кластерами HDInsight с помощью [пакета SDK для HDInsight.NET](https://msdn.microsoft.com/library/mt271028.aspx).

**Предварительные требования**

Перед началом работы с этой статьей необходимо иметь следующее:

* **Подписка Azure**. См. страницу [бесплатной пробной версии Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-to-azure-hdinsight"></a>Подключение к Azure HDInsight

Необходимо установить следующие пакеты NuGet:

```
Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
Install-Package Microsoft.Azure.Management.ResourceManager -Pre
Install-Package Microsoft.Azure.Management.HDInsight
```

В следующем примере кода показано, как подключиться к Azure, прежде чем администрировать кластеры HDInsight в подписке Azure.

```csharp
using System;
using Microsoft.Azure;
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Microsoft.Rest;
using Microsoft.Rest.Azure.Authentication;

namespace HDInsightManagement
{
    class Program
    {
        private static HDInsightManagementClient _hdiManagementClient;
        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId; 
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

        static void Main(string[] args)
        {
            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            // insert code here

            System.Console.WriteLine("Press ENTER to continue");
            System.Console.ReadLine();
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/", 
                ClientId, 
                new Uri("urn:ietf:wg:oauth:2.0:oob"), 
                PromptBehavior.Always, 
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
    }
}
```

При запуске этой программы появится запрос.  Если запрос не появится, обратитесь к статье [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Создание кластеров
Ознакомьтесь со статьей [Создание кластеров под управлением Linux в HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md).

## <a name="list-clusters"></a>Получение списка кластеров
В следующем фрагменте кода перечислены кластеры и некоторые свойства:

```csharp
var results = _hdiManagementClient.Clusters.List();
foreach (var name in results.Clusters) {
    Console.WriteLine("Cluster Name: " + name.Name);
    Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
    Console.WriteLine("\t Cluster location: " + name.Location);
    Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
}
```

## <a name="delete-clusters"></a>Удаление кластеров
Для синхронного или асинхронного удаления кластера используйте следующий фрагмент кода: 

```csharp
_hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
_hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");
```

## <a name="scale-clusters"></a>Масштабирование кластеров
Масштабирование кластера позволяет изменить количество рабочих узлов в кластере, который работает под управлением Azure HDInsight. При этом не требуется повторно создавать кластер.

> [!NOTE]
> Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней. Если вы не знаете версию кластера, см. страницу «Свойства».  См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

Ниже представлены возможности, связанные с изменением количества узлов данных в кластере каждого типа, поддерживаемого в HDInsight.

* Hadoop
  
    Вы можете легко увеличить количество рабочих узлов в работающем кластере Hadoop. Это не помешает обработке заданий в состоянии ожидания и выполнения. В ходе выполнения операции можно также отправлять новые задания. Сбои операции масштабирования обрабатываются корректно, поэтому кластер всегда пребывает в функциональном состоянии.
  
    Если уменьшить масштаб кластера Hadoop, сократив количество узлов данных, некоторые службы в нем будут перезапущены. Это приведет к сбою всех выполняющихся и ожидающих заданий при завершении операции масштабирования. Однако после завершения операции вы можете повторно отправить задания.
* hbase
  
    Вы можете с легкостью добавлять и удалять узлы данных в работающем кластере HBase. Балансировка региональных серверов выполняется автоматически в течение нескольких минут после завершения операции масштабирования. Но их также можно сбалансировать вручную, выполнив вход в головной узел кластера и выполнив следующие команды в окне командной строки:
  
    ```bash
    >pushd %HBASE_HOME%\bin
    >hbase shell
    >balancer
    ```
* Storm
  
    Вы можете с легкостью добавлять и удалять узлы данных в работающем кластере Storm. Но после успешного завершения операции масштабирования потребуется повторная балансировка топологии.
  
    Повторную балансировку можно выполнить двумя способами:
  
  * с помощью веб-интерфейса Storm;
  * с помощью программы командной строки.
    
    Дополнительные сведения см. в [документации по Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).
    
    В кластере HDInsight доступен веб-интерфейс Storm.
    
    ![HDInsight, Storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Ниже приведен пример использования команды CLI для повторной балансировки топологии Storm:
    
    ```cli
    ## Reconfigure the topology "mytopology" to use 5 worker processes,
    ## the spout "blue-spout" to use 3 executors, and
    ## the bolt "yellow-bolt" to use 10 executors
    $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10
    ```

В следующем фрагменте кода показано синхронное или асинхронное изменение размера кластера:

```csharp
_hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
_hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   
```

## <a name="grantrevoke-access"></a>Предоставление и отмена доступа
В кластерах HDInsight имеются следующие веб-службы HTTP (все эти службы имеют конечные точки RESTful):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

По умолчанию эти службы предоставляются для доступа. Вы можете отменить или предоставить доступ. Для отмены:

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = false,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

Для предоставления:

```csharp
var httpParams = new HttpSettingsParameters
{
    HttpUserEnabled = enable,
    HttpUsername = "admin",
    HttpPassword = "*******",
};
_hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);
```

> [!NOTE]
> Предоставляя или отменяя доступ, вы сбрасываете имя пользователя и пароль кластера.
> 
> 

Это также можно сделать через портал. Ознакомьтесь с разделом [Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Обновление учетных данных пользователя HTTP
Эта процедура аналогична [предоставлению или запрету доступа HTTP](#grant/revoke-access). Если кластеру был предоставлен доступ по протоколу HTTP, необходимо сначала отменить его.  После этого предоставьте доступ с новыми учетными данными пользователя HTTP.

## <a name="find-the-default-storage-account"></a>Поиск учетной записи хранения по умолчанию
В следующем фрагменте кода показано получение имени учетной записи хранения по умолчанию и ключа учетной записи хранения по умолчанию для кластера.

```csharp
var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
foreach (var key in results.Configuration.Keys)
{
    Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
}
```

## <a name="submit-jobs"></a>Отправка заданий
**Отправка заданий MapReduce**

См. статью [Выполнение примеров Hadoop в HDInsight](hadoop/apache-hadoop-run-samples-linux.md).

**Отправка заданий Hive** 

См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hadoop/apache-hadoop-use-hive-dotnet-sdk.md).

**Отправка заданий Pig**

См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hadoop/apache-hadoop-use-pig-dotnet-sdk.md).

**Отправка заданий Sqoop**

См. статью [Использование Sqoop с Hadoop в HDInsight](hadoop/apache-hadoop-use-sqoop-dotnet-sdk.md).

**Отправка заданий Oozie**

См. статью [Использование Oozie с Hadoop для определения и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-to-azure-blob-storage"></a>Отправка данных в хранилище BLOB-объектов Azure
Ознакомьтесь со статьей [Отправка данных в HDInsight][hdinsight-upload-data].

## <a name="see-also"></a>См. также
* [Справочная документация к пакету SDK для HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx)
* [Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal]
* [Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]
* [Создание кластеров Hadoop в HDInsight][hdinsight-provision]
* [Отправка данных в HDInsight][hdinsight-upload-data]
* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]:hadoop/submit-apache-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-mapreduce]:hadoop/hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


