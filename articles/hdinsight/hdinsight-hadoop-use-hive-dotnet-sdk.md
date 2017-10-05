---
title: "Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET — Azure | Документы Майкрософт"
description: "Узнайте, как отправлять задания Hadoop в Azure HDInsight Hadoop с помощью пакета SDK HDInsight для .NET."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 7b1a5f7ea3b2bda438727dc75a85557ea7930280
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="0ab7a-103">Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET</span><span class="sxs-lookup"><span data-stu-id="0ab7a-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="0ab7a-104">Узнайте, как отправлять запросы Hive с помощью пакета SDK HDInsight для .NET.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-104">Learn how to submit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="0ab7a-105">Напишите программу на языке C#, чтобы отправить запрос Hive для перечисления таблиц Hive и отобразить результаты.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-105">You write a C# program to submit a Hive query for listing Hive tables, and display the results.</span></span>

> [!NOTE]
> <span data-ttu-id="0ab7a-106">Действия, описанные в этой статье, необходимо выполнять из клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-106">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="0ab7a-107">Чтобы получить сведения об использовании клиента Linux, OS X или Unix для работы с Hive, воспользуйтесь выбором вкладок в верхней части статьи.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-107">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0ab7a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ab7a-108">Prerequisites</span></span>
<span data-ttu-id="0ab7a-109">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="0ab7a-109">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="0ab7a-110">**Кластер Hadoop в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="0ab7a-111">См. статью [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0ab7a-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="0ab7a-112">**Visual Studio 2013, Visual Studio 2015, Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="0ab7a-113">Отправка запросов Hive с помощью пакета SDK HDInsight для .NET</span><span class="sxs-lookup"><span data-stu-id="0ab7a-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="0ab7a-114">Пакет SDK для HDInsight .NET содержит клиентские библиотеки .NET, которые упрощают работу с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-114">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="0ab7a-115">**Отправка заданий**</span><span class="sxs-lookup"><span data-stu-id="0ab7a-115">**To Submit jobs**</span></span>

1. <span data-ttu-id="0ab7a-116">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="0ab7a-117">Введите следующую команду в окне консоли диспетчера пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="0ab7a-117">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="0ab7a-118">Используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0ab7a-118">Use the following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
   
        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
                private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
                private const string ExistingClusterUsername = "<Cluster Username>";
                private const string ExistingClusterPassword = "<Cluster User Password>";
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the Hive job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for the job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="0ab7a-119">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-119">Press **F5** to run the application.</span></span>

<span data-ttu-id="0ab7a-120">Выходные данные приложения должны иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="0ab7a-120">The output of the application shall be similar to:</span></span>

![Выходные данные задания Hadoop Hive в HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="0ab7a-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ab7a-122">Next steps</span></span>
<span data-ttu-id="0ab7a-123">В этой статье вы ознакомились с несколькими способами создания кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ab7a-123">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="0ab7a-124">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="0ab7a-124">To learn more, see the following articles:</span></span>

* <span data-ttu-id="0ab7a-125">[Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0ab7a-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="0ab7a-126">[Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="0ab7a-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="0ab7a-127">Управление кластерами Hadoop в HDInsight с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="0ab7a-127">Manage Hadoop clusters in HDInsight by using the Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="0ab7a-128">Справочник по пакетам SDK HDInsight для .NET</span><span class="sxs-lookup"><span data-stu-id="0ab7a-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="0ab7a-129">Использование Pig с HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ab7a-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0ab7a-130">Использование Sqoop с HDInsight</span><span class="sxs-lookup"><span data-stu-id="0ab7a-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="0ab7a-131">Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности</span><span class="sxs-lookup"><span data-stu-id="0ab7a-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


