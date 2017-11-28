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
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="48034-103">Управление кластерами Hadoop в HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="48034-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="48034-104">Научитесь управлять кластерами HDInsight с помощью [пакета SDK для HDInsight.NET](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="48034-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="48034-105">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="48034-105">**Prerequisites**</span></span>

<span data-ttu-id="48034-106">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="48034-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="48034-107">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="48034-107">**An Azure subscription**.</span></span> <span data-ttu-id="48034-108">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="48034-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="48034-109">Подключение к Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="48034-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="48034-110">Необходимо установить следующие пакеты Nuget:</span><span class="sxs-lookup"><span data-stu-id="48034-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="48034-111">В следующем примере кода показано, как подключиться к Azure, прежде чем администрировать кластеры HDInsight в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="48034-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="48034-112">При запуске этой программы появится запрос.</span><span class="sxs-lookup"><span data-stu-id="48034-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="48034-113">Если запрос не появится, обратитесь к статье [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="48034-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="48034-114">Создание кластеров</span><span class="sxs-lookup"><span data-stu-id="48034-114">Create clusters</span></span>
<span data-ttu-id="48034-115">Ознакомьтесь со статьей [Создание кластеров под управлением Linux в HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="48034-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="48034-116">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="48034-116">List clusters</span></span>
<span data-ttu-id="48034-117">В следующем фрагменте кода перечислены кластеры и некоторые свойства:</span><span class="sxs-lookup"><span data-stu-id="48034-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="48034-118">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="48034-118">Delete clusters</span></span>
<span data-ttu-id="48034-119">Для синхронного или асинхронного удаления кластера используйте следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="48034-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="48034-120">Масштабирование кластеров</span><span class="sxs-lookup"><span data-stu-id="48034-120">Scale clusters</span></span>
<span data-ttu-id="48034-121">Масштабирование кластера позволяет изменить количество рабочих узлов в кластере, который работает под управлением Azure HDInsight. При этом не требуется повторно создавать кластер.</span><span class="sxs-lookup"><span data-stu-id="48034-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="48034-122">Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="48034-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="48034-123">Если вы не знаете версию кластера, см. страницу «Свойства».</span><span class="sxs-lookup"><span data-stu-id="48034-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="48034-124">См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="48034-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="48034-125">Ниже представлены возможности, связанные с изменением количества узлов данных в кластере каждого типа, поддерживаемого в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="48034-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="48034-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="48034-126">Hadoop</span></span>
  
    <span data-ttu-id="48034-127">Вы можете легко увеличить количество рабочих узлов в работающем кластере Hadoop. Это не помешает обработке заданий в состоянии ожидания и выполнения.</span><span class="sxs-lookup"><span data-stu-id="48034-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="48034-128">В ходе выполнения операции можно также отправлять новые задания.</span><span class="sxs-lookup"><span data-stu-id="48034-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="48034-129">Сбои операции масштабирования обрабатываются корректно, поэтому кластер всегда пребывает в функциональном состоянии.</span><span class="sxs-lookup"><span data-stu-id="48034-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="48034-130">Если уменьшить масштаб кластера Hadoop, сократив количество узлов данных, некоторые службы в нем будут перезапущены.</span><span class="sxs-lookup"><span data-stu-id="48034-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="48034-131">Это приведет к сбою всех выполняющихся и ожидающих заданий при завершении операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="48034-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="48034-132">Однако после завершения операции вы можете повторно отправить задания.</span><span class="sxs-lookup"><span data-stu-id="48034-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="48034-133">HBase</span><span class="sxs-lookup"><span data-stu-id="48034-133">HBase</span></span>
  
    <span data-ttu-id="48034-134">Вы можете с легкостью добавлять и удалять узлы данных в работающем кластере HBase.</span><span class="sxs-lookup"><span data-stu-id="48034-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="48034-135">Балансировка региональных серверов выполняется автоматически в течение нескольких минут после завершения операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="48034-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="48034-136">Но их также можно сбалансировать вручную, выполнив вход в головной узел кластера и выполнив следующие команды в окне командной строки:</span><span class="sxs-lookup"><span data-stu-id="48034-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="48034-137">Storm</span><span class="sxs-lookup"><span data-stu-id="48034-137">Storm</span></span>
  
    <span data-ttu-id="48034-138">Вы можете с легкостью добавлять и удалять узлы данных в работающем кластере Storm.</span><span class="sxs-lookup"><span data-stu-id="48034-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="48034-139">Но после успешного завершения операции масштабирования потребуется повторная балансировка топологии.</span><span class="sxs-lookup"><span data-stu-id="48034-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="48034-140">Повторную балансировку можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="48034-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="48034-141">с помощью веб-интерфейса Storm;</span><span class="sxs-lookup"><span data-stu-id="48034-141">Storm web UI</span></span>
  * <span data-ttu-id="48034-142">с помощью программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="48034-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="48034-143">Дополнительные сведения см. в [документации по Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="48034-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="48034-144">В кластере HDInsight доступен веб-интерфейс Storm.</span><span class="sxs-lookup"><span data-stu-id="48034-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![HDInsight, Storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="48034-146">Ниже приведен пример использования команды CLI для повторной балансировки топологии Storm:</span><span class="sxs-lookup"><span data-stu-id="48034-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="48034-147">В следующем фрагменте кода показано синхронное или асинхронное изменение размера кластера:</span><span class="sxs-lookup"><span data-stu-id="48034-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="48034-148">Предоставление и отмена доступа</span><span class="sxs-lookup"><span data-stu-id="48034-148">Grant/revoke access</span></span>
<span data-ttu-id="48034-149">В кластерах HDInsight имеются следующие веб-службы HTTP (все эти службы имеют конечные точки RESTful):</span><span class="sxs-lookup"><span data-stu-id="48034-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="48034-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="48034-150">ODBC</span></span>
* <span data-ttu-id="48034-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="48034-151">JDBC</span></span>
* <span data-ttu-id="48034-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="48034-152">Ambari</span></span>
* <span data-ttu-id="48034-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="48034-153">Oozie</span></span>
* <span data-ttu-id="48034-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="48034-154">Templeton</span></span>

<span data-ttu-id="48034-155">По умолчанию эти службы предоставляются для доступа.</span><span class="sxs-lookup"><span data-stu-id="48034-155">By default, these services are granted for access.</span></span> <span data-ttu-id="48034-156">Вы можете отменить или предоставить доступ.</span><span class="sxs-lookup"><span data-stu-id="48034-156">You can revoke/grant the access.</span></span> <span data-ttu-id="48034-157">Для отмены:</span><span class="sxs-lookup"><span data-stu-id="48034-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="48034-158">Для предоставления:</span><span class="sxs-lookup"><span data-stu-id="48034-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="48034-159">Предоставляя или отменяя доступ, вы сбрасываете имя пользователя и пароль кластера.</span><span class="sxs-lookup"><span data-stu-id="48034-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="48034-160">Это также можно сделать через портал.</span><span class="sxs-lookup"><span data-stu-id="48034-160">This can also be done via the Portal.</span></span> <span data-ttu-id="48034-161">Ознакомьтесь с разделом [Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="48034-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="48034-162">Обновление учетных данных пользователя HTTP</span><span class="sxs-lookup"><span data-stu-id="48034-162">Update HTTP user credentials</span></span>
<span data-ttu-id="48034-163">Эта процедура аналогична [предоставлению или запрету доступа HTTP](#grant/revoke-access). Если кластеру был предоставлен доступ по протоколу HTTP, необходимо сначала отменить его.</span><span class="sxs-lookup"><span data-stu-id="48034-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="48034-164">После этого предоставьте доступ с новыми учетными данными пользователя HTTP.</span><span class="sxs-lookup"><span data-stu-id="48034-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="48034-165">Поиск учетной записи хранения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="48034-165">Find the default storage account</span></span>
<span data-ttu-id="48034-166">В следующем фрагменте кода показано получение имени учетной записи хранения по умолчанию и ключа учетной записи хранения по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="48034-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="48034-167">Отправка заданий</span><span class="sxs-lookup"><span data-stu-id="48034-167">Submit jobs</span></span>
<span data-ttu-id="48034-168">**Отправка заданий MapReduce**</span><span class="sxs-lookup"><span data-stu-id="48034-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="48034-169">См. статью [Выполнение примеров Hadoop в HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="48034-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="48034-170">**Отправка заданий Hive**</span><span class="sxs-lookup"><span data-stu-id="48034-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="48034-171">См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="48034-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="48034-172">**Отправка заданий Pig**</span><span class="sxs-lookup"><span data-stu-id="48034-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="48034-173">См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="48034-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="48034-174">**Отправка заданий Sqoop**</span><span class="sxs-lookup"><span data-stu-id="48034-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="48034-175">См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="48034-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="48034-176">**Отправка заданий Oozie**</span><span class="sxs-lookup"><span data-stu-id="48034-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="48034-177">См. статью [Использование Oozie с Hadoop для определения и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="48034-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="48034-178">Отправка данных в хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="48034-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="48034-179">Ознакомьтесь со статьей [Отправка данных в HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="48034-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="48034-180">См. также</span><span class="sxs-lookup"><span data-stu-id="48034-180">See Also</span></span>
* [<span data-ttu-id="48034-181">Справочная документация к пакету SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="48034-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="48034-182">[Администрирование HDInsight с помощью портала Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="48034-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="48034-183">[Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="48034-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="48034-184">[Создание кластеров Hadoop в HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="48034-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="48034-185">[Отправка данных в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="48034-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="48034-186">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="48034-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


