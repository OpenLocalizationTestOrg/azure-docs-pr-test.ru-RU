---
title: "HDInsight .NET SDK - Azure с помощью запросов Hive aaaRun | Документы Microsoft"
description: "Узнайте, как toosubmit Hadoop задания tooAzure HDInsight Hadoop с помощью HDInsight .NET SDK."
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
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Выполнение запросов Hive с помощью пакета SDK HDInsight для .NET
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Узнайте, как toosubmit Hive запросов с помощью HDInsight .NET SDK. Написать запрос Hive для перечисления таблиц куст toosubmit программы C# и отображение результатов hello.

> [!NOTE]
> в этой статье инструкциям Hello должна быть выполнена из клиента Windows. Сведения об использовании Linux, OS X или toowork клиента Unix с Hive с помощью селектора вкладку hello, отображается в верхней части hello hello статьи.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь hello следующих элементов:

* **Кластер Hadoop в HDInsight**. См. статью [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013, Visual Studio 2015, Visual Studio 2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Отправка запросов Hive с помощью пакета SDK HDInsight для .NET
Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET. 

**tooSubmit заданий**

1. Создайте в Visual Studio консольное приложение C#.
2. В hello консоль диспетчера пакетов Nuget выполните следующую команду hello.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Используйте hello, следующий код:

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
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
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
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
4. Нажмите клавишу **F5** toorun приложения hello.

выходные данные Hello приложения hello должны выглядеть следующим образом:

![Выходные данные задания Hadoop Hive в HDInsight](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Дальнейшие действия
В этой статье было изучено несколько способов toocreate кластера HDInsight. toolearn более, см. следующие статьи hello.

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux][hdinsight-get-started]
* [Создание кластеров Hadoop под управлением Windows в HDInsight][hdinsight-provision]
* [Управление кластерами Hadoop в HDInsight с помощью портала Azure hello](hdinsight-administer-use-management-portal.md)
* [Справочник по пакетам SDK HDInsight для .NET](https://msdn.microsoft.com/library/mt271028.aspx)
* [Использование Pig с HDInsight](hdinsight-use-pig.md)
* [Использование Sqoop с HDInsight](hdinsight-use-sqoop-mac-linux.md)
* [Создание приложений .NET HDInsight с неинтерактивной проверкой подлинности](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


