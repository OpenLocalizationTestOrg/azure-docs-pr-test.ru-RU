---
title: "Отправка заданий MapReduce с использованием пакета SDK HDInsight для .NET — Azure | Документы Майкрософт"
description: "Узнайте, как отправлять задания MapReduce в Azure HDInsight Hadoop с использованием пакета SDK для HDInsight .NET."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 015435270c31bafea0ebf5303b459338755c1410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="0cb4f-103">Выполнение заданий MapReduce с использованием пакета SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="0cb4f-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="0cb4f-104">Узнайте, как отправлять задания MapReduce с использованием пакета SDK для HDInsight .NET.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-104">Learn how to submit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="0cb4f-105">В кластерах HDInsight предусмотрен JAR-файл с несколькими примерами MapReduce.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="0cb4f-106">Этот JAR-файл — */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-106">The jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="0cb4f-107">Один из примеров — *wordcount* (подсчет слов).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-107">One of the samples is *wordcount*.</span></span> <span data-ttu-id="0cb4f-108">Вы разрабатываете консольное приложение на C# для отправки задания по подсчету слов.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-108">You develop a C# console application to submit a wordcount job.</span></span>  <span data-ttu-id="0cb4f-109">Задание считывает файл */example/data/gutenberg/davinci.txt* и сохраняет результат в */example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-109">The job reads the */example/data/gutenberg/davinci.txt* file, and outputs the results to */example/data/davinciwordcount*.</span></span>  <span data-ttu-id="0cb4f-110">Чтобы снова запустить приложение, необходимо очистить папку выходных данных.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-110">If you want to rerun the application, you must clean up the output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="0cb4f-111">Действия, описанные в этой статье, необходимо выполнять из клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-111">The steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="0cb4f-112">Чтобы получить сведения об использовании клиента Linux, OS X или Unix для работы с Hive, воспользуйтесь выбором вкладок в верхней части статьи.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-112">For information on using a Linux, OS X, or Unix client to work with Hive, use the tab selector shown on the top of the article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0cb4f-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0cb4f-113">Prerequisites</span></span>
<span data-ttu-id="0cb4f-114">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="0cb4f-114">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="0cb4f-115">**Кластер Hadoop в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="0cb4f-116">См. статью [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="0cb4f-117">**Visual Studio 2013, Visual Studio 2015, Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="0cb4f-118">Отправка заданий MapReduce с использованием пакета SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="0cb4f-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="0cb4f-119">Пакет SDK для HDInsight .NET содержит клиентские библиотеки .NET, которые упрощают работу с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-119">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="0cb4f-120">**Отправка заданий**</span><span class="sxs-lookup"><span data-stu-id="0cb4f-120">**To Submit jobs**</span></span>

1. <span data-ttu-id="0cb4f-121">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="0cb4f-122">Введите следующую команду в окне консоли диспетчера пакетов NuGet:</span><span class="sxs-lookup"><span data-stu-id="0cb4f-122">From the Nuget Package Manager Console, run the following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="0cb4f-123">Используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="0cb4f-123">Use the following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting the MR job to the cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create the storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create the blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference to a previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="0cb4f-124">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-124">Press **F5** to run the application.</span></span>

<span data-ttu-id="0cb4f-125">Чтобы снова запустить задание, необходимо изменить имя выходной папки задания. В нашем примере это /example/data/davinciwordcount.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-125">To run the job again, you must change the job output folder name, in the sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="0cb4f-126">По завершении задания приложение печатает содержимое выходного файла part-r-00000.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-126">When the job completes successfully, the application prints the content of the output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cb4f-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0cb4f-127">Next steps</span></span>
<span data-ttu-id="0cb4f-128">В этой статье вы ознакомились с несколькими способами создания кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0cb4f-128">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="0cb4f-129">Для получения дополнительных сведений ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="0cb4f-129">To learn more, see the following articles:</span></span>

* <span data-ttu-id="0cb4f-130">Сведения об отправке задания Hive см. в инструкциях по [выполнению запросов Hive с помощью пакета SDK для HDInsight .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="0cb4f-131">Сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="0cb4f-132">Сведения об управлении кластерами в HDInsight см. в статье [Управление кластерами Hadoop в HDInsight с помощью портала Azure](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="0cb4f-133">Подробные сведения о пакете SDK для HDInsight .NET см. в [соответствующей справке](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-133">For learning the HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="0cb4f-134">Сведения о неинтерактивной проверке подлинности в Azure см. в статье [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4f-134">For non-interactive authenticate to Azure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

