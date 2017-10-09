---
title: "кластеры aaaManage Hadoop в HDInsight с помощью пакета SDK для .NET - Azure | Документы Microsoft"
description: "Узнайте, как tooperform административные задачи для hello кластеров Hadoop в HDInsight с помощью HDInsight .NET SDK."
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
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a>Управление кластерами Hadoop в HDInsight с помощью пакета SDK для .NET
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Узнайте, как toomanage HDInsight кластеры, использующие [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).

**Предварительные требования**

Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="connect-tooazure-hdinsight"></a>Подключение tooAzure HDInsight

Необходимы следующие пакеты Nuget hello.

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

Hello следующем образце кода показано, как кластеры tooAzure tooconnect Администрирование HDInsight под вашей подпиской Azure.

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
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
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
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

При запуске этой программы появится запрос.  Если вы не хотите toosee hello строки, см. раздел [создавать неинтерактивной проверки подлинности приложений .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

## <a name="create-clusters"></a>Создание кластеров
В разделе [Здравствуйте, под управлением Linux, создание кластеров HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)

## <a name="list-clusters"></a>Получение списка кластеров
Hello следующий фрагмент кода список кластеров и некоторые свойства:

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a>Удаление кластеров
Используйте hello, следующий фрагмент кода toodelete кластера синхронно или асинхронно. 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a>Масштабирование кластеров
масштабирование функции кластера Hello позволяет toochange hello число рабочих узлов в кластере, который выполняется в Azure HDInsight без необходимости toore-создать кластер hello.

> [!NOTE]
> Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней. Если вы не знаете hello версии кластера, можно проверить свойства страницы приветствия.  См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
> 
> 

Hello последствия изменения hello количество узлов данных для каждого типа поддерживаемых HDInsight кластера:

* Hadoop
  
    Можно легко увеличить hello число рабочих узлов в кластере Hadoop, на котором выполняется без ущерба для все ожидающие или выполняемые задания. Также можно отправлять новые задания, hello операции во время выполнения. Ошибки в операции масштабирования обрабатываются правильно, чтобы hello кластер всегда оставался в рабочем состоянии.
  
    Когда кластер Hadoop уменьшено за счет уменьшения hello количество узлов данных, некоторые службы hello в кластере hello перезапускаются. В результате все выполняющиеся и ожидающие задания toofail окончании hello hello операцию масштабирования. Можно Однако повторно отправить задания hello после завершения операции hello.
* HBase
  
    Можно легко добавить или удалить узлы tooyour HBase кластера при выполнении. Региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования. Тем не менее можно также вручную сбалансировать региональные серверы hello, войдя в hello головному узлу кластера, и выполнение hello, следующие команды из окна командной строки:
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm
  
    Можно легко добавить или удалить кластер Storm tooyour узлы данных при выполнении. Однако после успешного завершения hello операция масштабирования потребуется toorebalance hello топологии.
  
    Повторную балансировку можно выполнить двумя способами:
  
  * с помощью веб-интерфейса Storm;
  * с помощью программы командной строки.
    
    См. toohello [документации Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) для получения дополнительных сведений.
    
    в кластере HDInsight hello доступен Hello Storm пользовательского веб-интерфейса:
    
    ![HDInsight, Storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    Ниже приведен пример как toouse hello CLI команды toorebalance hello Storm топологии:
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Здравствуйте, в следующем фрагменте кода показан код как tooresize кластера синхронно или асинхронно:

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a>Предоставление и отмена доступа
Кластеры HDInsight имеют hello следующие веб-службы HTTP (все эти службы имеют RESTful конечные точки):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

По умолчанию эти службы предоставляются для доступа. Вы можете revoke или предоставления доступа hello. toorevoke:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

toogrant:

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> Предоставление или Отмена доступа hello, восстановится hello кластера имя и пароль пользователя.
> 
> 

Это можно сделать через портал hello. В разделе [Здравствуйте, администрировать HDInsight с помощью портала Azure][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>Обновление учетных данных пользователя HTTP
Это же hello процедуры как [доступа для предоставления или отзыва HTTP](#grant/revoke-access). Если кластер hello было предоставлено hello доступа по протоколу HTTP, то необходимо отозвать.  А затем предоставить доступ hello с новыми учетными данными пользователя HTTP.

## <a name="find-hello-default-storage-account"></a>Найти учетную запись хранения по умолчанию hello
Следующий фрагмент кода Hello демонстрируется tooget имя учетной записи хранения по умолчанию hello и hello ключ учетной записи хранения по умолчанию для кластера.

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a>Отправка заданий
**задания MapReduce toosubmit**

См. статью [Выполнение примеров Hadoop в HDInsight](hdinsight-hadoop-run-samples-linux.md).

**задания Hive toosubmit** 

См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).

**задания Pig toosubmit**

См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).

**toosubmit Sqoop заданий**

См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).

**toosubmit Oozie заданий**

В разделе [Oozie использования с Hadoop toodefine и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie-linux-mac.md).

## <a name="upload-data-tooazure-blob-storage"></a>Отправка больших двоичных объектов хранилища данных tooAzure
В разделе [отправить данные tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>См. также
* [Справочная документация к пакету SDK для HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx)
* [Администрирование с помощью hello портал Azure HDInsight][hdinsight-admin-portal]
* [Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]
* [Создание кластеров Hadoop в HDInsight][hdinsight-provision]
* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


