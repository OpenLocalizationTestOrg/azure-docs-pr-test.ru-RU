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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Выполнение заданий MapReduce с использованием пакета SDK для HDInsight .NET
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Узнайте, как toosubmit MapReduce заданий с помощью HDInsight .NET SDK. В кластерах HDInsight предусмотрен JAR-файл с несколькими примерами MapReduce. Hello jar-файл является */example/jars/hadoop-mapreduce-examples.jar*.  Одним из примеров hello является *wordcount*. Разработка C# консольного приложения toosubmit wordcount задания.  Задание Hello считывает hello */example/data/gutenberg/davinci.txt* файл и выводит hello результатов слишком*/example/data/davinciwordcount*.  Если требуется, чтобы приложение hello toorerun, необходимо очистить hello выходную папку.

> [!NOTE]
> в этой статье инструкциям Hello должна быть выполнена из клиента Windows. Сведения об использовании Linux, OS X или toowork клиента Unix с Hive с помощью селектора вкладку hello, отображается в верхней части hello hello статьи.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:

* **Кластер Hadoop в HDInsight**. См. статью [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013, Visual Studio 2015, Visual Studio 2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Отправка заданий MapReduce с использованием пакета SDK для HDInsight .NET
Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET. 

**tooSubmit заданий**

1. Создайте в Visual Studio консольное приложение C#.
2. В hello консоль диспетчера пакетов Nuget выполните следующую команду hello.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Используйте hello, следующий код:
   
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
4. Нажмите клавишу **F5** toorun приложения hello.

Задание hello toorun еще раз, необходимо изменить hello выходной папки имя задания, в образце hello, это «/ пример, данных или davinciwordcount».

По завершении заданий hello приложение hello выводит содержимое hello hello выходного файла «часть r-00000».

## <a name="next-steps"></a>Дальнейшие действия
В этой статье было изучено несколько способов toocreate кластера HDInsight. toolearn более, см. следующие статьи hello.

* Сведения об отправке задания Hive см. в инструкциях по [выполнению запросов Hive с помощью пакета SDK для HDInsight .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Сведения о создании кластеров HDInsight см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Сведения об управлении кластерами в HDInsight см. в статье [Управление кластерами Hadoop в HDInsight с помощью портала Azure](hdinsight-administer-use-portal-linux.md).
* Обучение hello HDInsight .NET SDK, в разделе [HDInsight .NET SDK ссылка](https://msdn.microsoft.com/library/mt271028.aspx).
* Для неинтерактивной tooAzure проверки подлинности см. в разделе [создавать неинтерактивной проверки подлинности приложений .NET HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

