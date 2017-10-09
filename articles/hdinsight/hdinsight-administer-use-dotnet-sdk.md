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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="0f2f7-103">Управление кластерами Hadoop в HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="0f2f7-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="0f2f7-104">Узнайте, как toomanage HDInsight кластеры, использующие [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="0f2f7-105">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="0f2f7-105">**Prerequisites**</span></span>

<span data-ttu-id="0f2f7-106">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="0f2f7-107">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-107">**An Azure subscription**.</span></span> <span data-ttu-id="0f2f7-108">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="0f2f7-109">Подключение tooAzure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f2f7-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="0f2f7-110">Необходимы следующие пакеты Nuget hello.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="0f2f7-111">Hello следующем образце кода показано, как кластеры tooAzure tooconnect Администрирование HDInsight под вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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

<span data-ttu-id="0f2f7-112">При запуске этой программы появится запрос.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="0f2f7-113">Если вы не хотите toosee hello строки, см. раздел [создавать неинтерактивной проверки подлинности приложений .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="0f2f7-114">Создание кластеров</span><span class="sxs-lookup"><span data-stu-id="0f2f7-114">Create clusters</span></span>
<span data-ttu-id="0f2f7-115">В разделе [Здравствуйте, под управлением Linux, создание кластеров HDInsight с помощью пакета SDK для .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="0f2f7-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="0f2f7-116">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="0f2f7-116">List clusters</span></span>
<span data-ttu-id="0f2f7-117">Hello следующий фрагмент кода список кластеров и некоторые свойства:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="0f2f7-118">Удаление кластеров</span><span class="sxs-lookup"><span data-stu-id="0f2f7-118">Delete clusters</span></span>
<span data-ttu-id="0f2f7-119">Используйте hello, следующий фрагмент кода toodelete кластера синхронно или асинхронно.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="0f2f7-120">Масштабирование кластеров</span><span class="sxs-lookup"><span data-stu-id="0f2f7-120">Scale clusters</span></span>
<span data-ttu-id="0f2f7-121">масштабирование функции кластера Hello позволяет toochange hello число рабочих узлов в кластере, который выполняется в Azure HDInsight без необходимости toore-создать кластер hello.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2f7-122">Поддерживаются только кластеры HDInsight версии 3.1.3 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="0f2f7-123">Если вы не знаете hello версии кластера, можно проверить свойства страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="0f2f7-124">См. раздел [Отображение кластеров](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="0f2f7-125">Hello последствия изменения hello количество узлов данных для каждого типа поддерживаемых HDInsight кластера:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="0f2f7-126">Hadoop</span><span class="sxs-lookup"><span data-stu-id="0f2f7-126">Hadoop</span></span>
  
    <span data-ttu-id="0f2f7-127">Можно легко увеличить hello число рабочих узлов в кластере Hadoop, на котором выполняется без ущерба для все ожидающие или выполняемые задания.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="0f2f7-128">Также можно отправлять новые задания, hello операции во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="0f2f7-129">Ошибки в операции масштабирования обрабатываются правильно, чтобы hello кластер всегда оставался в рабочем состоянии.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="0f2f7-130">Когда кластер Hadoop уменьшено за счет уменьшения hello количество узлов данных, некоторые службы hello в кластере hello перезапускаются.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="0f2f7-131">В результате все выполняющиеся и ожидающие задания toofail окончании hello hello операцию масштабирования.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="0f2f7-132">Можно Однако повторно отправить задания hello после завершения операции hello.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="0f2f7-133">HBase</span><span class="sxs-lookup"><span data-stu-id="0f2f7-133">HBase</span></span>
  
    <span data-ttu-id="0f2f7-134">Можно легко добавить или удалить узлы tooyour HBase кластера при выполнении.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="0f2f7-135">Региональные серверы распределяются автоматически через несколько минут после завершения hello операция масштабирования.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="0f2f7-136">Тем не менее можно также вручную сбалансировать региональные серверы hello, войдя в hello головному узлу кластера, и выполнение hello, следующие команды из окна командной строки:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="0f2f7-137">Storm</span><span class="sxs-lookup"><span data-stu-id="0f2f7-137">Storm</span></span>
  
    <span data-ttu-id="0f2f7-138">Можно легко добавить или удалить кластер Storm tooyour узлы данных при выполнении.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="0f2f7-139">Однако после успешного завершения hello операция масштабирования потребуется toorebalance hello топологии.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="0f2f7-140">Повторную балансировку можно выполнить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="0f2f7-141">с помощью веб-интерфейса Storm;</span><span class="sxs-lookup"><span data-stu-id="0f2f7-141">Storm web UI</span></span>
  * <span data-ttu-id="0f2f7-142">с помощью программы командной строки.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="0f2f7-143">См. toohello [документации Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="0f2f7-144">в кластере HDInsight hello доступен Hello Storm пользовательского веб-интерфейса:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![HDInsight, Storm, масштабирование, перераспределение](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="0f2f7-146">Ниже приведен пример как toouse hello CLI команды toorebalance hello Storm топологии:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="0f2f7-147">Здравствуйте, в следующем фрагменте кода показан код как tooresize кластера синхронно или асинхронно:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="0f2f7-148">Предоставление и отмена доступа</span><span class="sxs-lookup"><span data-stu-id="0f2f7-148">Grant/revoke access</span></span>
<span data-ttu-id="0f2f7-149">Кластеры HDInsight имеют hello следующие веб-службы HTTP (все эти службы имеют RESTful конечные точки):</span><span class="sxs-lookup"><span data-stu-id="0f2f7-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="0f2f7-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="0f2f7-150">ODBC</span></span>
* <span data-ttu-id="0f2f7-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="0f2f7-151">JDBC</span></span>
* <span data-ttu-id="0f2f7-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="0f2f7-152">Ambari</span></span>
* <span data-ttu-id="0f2f7-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="0f2f7-153">Oozie</span></span>
* <span data-ttu-id="0f2f7-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="0f2f7-154">Templeton</span></span>

<span data-ttu-id="0f2f7-155">По умолчанию эти службы предоставляются для доступа.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-155">By default, these services are granted for access.</span></span> <span data-ttu-id="0f2f7-156">Вы можете revoke или предоставления доступа hello.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="0f2f7-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="0f2f7-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="0f2f7-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="0f2f7-159">Предоставление или Отмена доступа hello, восстановится hello кластера имя и пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="0f2f7-160">Это можно сделать через портал hello.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="0f2f7-161">В разделе [Здравствуйте, администрировать HDInsight с помощью портала Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="0f2f7-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="0f2f7-162">Обновление учетных данных пользователя HTTP</span><span class="sxs-lookup"><span data-stu-id="0f2f7-162">Update HTTP user credentials</span></span>
<span data-ttu-id="0f2f7-163">Это же hello процедуры как [доступа для предоставления или отзыва HTTP](#grant/revoke-access). Если кластер hello было предоставлено hello доступа по протоколу HTTP, то необходимо отозвать.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="0f2f7-164">А затем предоставить доступ hello с новыми учетными данными пользователя HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="0f2f7-165">Найти учетную запись хранения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="0f2f7-165">Find hello default storage account</span></span>
<span data-ttu-id="0f2f7-166">Следующий фрагмент кода Hello демонстрируется tooget имя учетной записи хранения по умолчанию hello и hello ключ учетной записи хранения по умолчанию для кластера.</span><span class="sxs-lookup"><span data-stu-id="0f2f7-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="0f2f7-167">Отправка заданий</span><span class="sxs-lookup"><span data-stu-id="0f2f7-167">Submit jobs</span></span>
<span data-ttu-id="0f2f7-168">**задания MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="0f2f7-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="0f2f7-169">См. статью [Выполнение примеров Hadoop в HDInsight](hdinsight-hadoop-run-samples-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="0f2f7-170">**задания Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="0f2f7-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="0f2f7-171">См. статью [Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="0f2f7-172">**задания Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="0f2f7-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="0f2f7-173">См. статью [Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="0f2f7-174">**toosubmit Sqoop заданий**</span><span class="sxs-lookup"><span data-stu-id="0f2f7-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="0f2f7-175">См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="0f2f7-176">**toosubmit Oozie заданий**</span><span class="sxs-lookup"><span data-stu-id="0f2f7-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="0f2f7-177">В разделе [Oozie использования с Hadoop toodefine и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="0f2f7-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="0f2f7-178">Отправка больших двоичных объектов хранилища данных tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f2f7-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="0f2f7-179">В разделе [отправить данные tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="0f2f7-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="0f2f7-180">См. также</span><span class="sxs-lookup"><span data-stu-id="0f2f7-180">See Also</span></span>
* [<span data-ttu-id="0f2f7-181">Справочная документация к пакету SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="0f2f7-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="0f2f7-182">[Администрирование с помощью hello портал Azure HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="0f2f7-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="0f2f7-183">[Администрирование HDInsight с помощью интерфейса командной строки][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="0f2f7-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="0f2f7-184">[Создание кластеров Hadoop в HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="0f2f7-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="0f2f7-185">[Отправка данных tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="0f2f7-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="0f2f7-186">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0f2f7-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


