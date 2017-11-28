---
title: "HDInsight .NET SDK - Azure с помощью задания MapReduce aaaSubmit | Документы Microsoft"
description: "Узнайте, как toosubmit MapReduce заданий tooAzure HDInsight Hadoop с помощью HDInsight .NET SDK."
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
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="56777-103">Выполнение заданий MapReduce с использованием пакета SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="56777-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="56777-104">Узнайте, как toosubmit MapReduce заданий с помощью HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="56777-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="56777-105">В кластерах HDInsight предусмотрен JAR-файл с несколькими примерами MapReduce.</span><span class="sxs-lookup"><span data-stu-id="56777-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="56777-106">Hello jar-файл является */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="56777-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="56777-107">Одним из примеров hello является *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="56777-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="56777-108">Разработка C# консольного приложения toosubmit wordcount задания.</span><span class="sxs-lookup"><span data-stu-id="56777-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="56777-109">Задание Hello считывает hello */example/data/gutenberg/davinci.txt* файл и выводит hello результатов слишком*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="56777-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="56777-110">Если требуется, чтобы приложение hello toorerun, необходимо очистить hello выходную папку.</span><span class="sxs-lookup"><span data-stu-id="56777-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="56777-111">в этой статье инструкциям Hello должна быть выполнена из клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="56777-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="56777-112">Сведения об использовании Linux, OS X или toowork клиента Unix с Hive с помощью селектора вкладку hello, отображается в верхней части hello hello статьи.</span><span class="sxs-lookup"><span data-stu-id="56777-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="56777-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="56777-113">Prerequisites</span></span>
<span data-ttu-id="56777-114">Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="56777-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="56777-115">**Кластер Hadoop в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="56777-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="56777-116">См. статью [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="56777-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="56777-117">**Visual Studio 2013, Visual Studio 2015, Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="56777-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="56777-118">Отправка заданий MapReduce с использованием пакета SDK для HDInsight .NET</span><span class="sxs-lookup"><span data-stu-id="56777-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="56777-119">Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="56777-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="56777-120">**tooSubmit заданий**</span><span class="sxs-lookup"><span data-stu-id="56777-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="56777-121">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="56777-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="56777-122">В hello консоль диспетчера пакетов Nuget выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="56777-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="56777-123">Используйте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="56777-123">Use hello following code:</span></span>
   
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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
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
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
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
4. <span data-ttu-id="56777-124">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="56777-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="56777-125">Задание hello toorun еще раз, необходимо изменить hello выходной папки имя задания, в образце hello, это «/ пример, данных или davinciwordcount».</span><span class="sxs-lookup"><span data-stu-id="56777-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="56777-126">По завершении заданий hello приложение hello выводит содержимое hello hello выходного файла «часть r-00000».</span><span class="sxs-lookup"><span data-stu-id="56777-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="56777-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56777-127">Next steps</span></span>
<span data-ttu-id="56777-128">В этой статье было изучено несколько способов toocreate кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="56777-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="56777-129">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="56777-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="56777-130">Сведения об отправке задания Hive см. в инструкциях по [выполнению запросов Hive с помощью пакета SDK для HDInsight .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="56777-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="56777-131">Сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="56777-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="56777-132">Сведения об управлении кластерами в HDInsight см. в статье [Управление кластерами Hadoop в HDInsight с помощью портала Azure](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="56777-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="56777-133">Обучение hello HDInsight .NET SDK, в разделе [HDInsight .NET SDK ссылка](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="56777-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="56777-134">Для неинтерактивной tooAzure проверки подлинности см. в разделе [создавать неинтерактивной проверки подлинности приложений .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="56777-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

