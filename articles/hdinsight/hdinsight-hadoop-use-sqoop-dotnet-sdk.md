---
title: "aaaRun Sqoop заданий с помощью .NET и HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как toorun HDInsight .NET SDK toouse Sqoop Импорт и экспорт между кластера Hadoop и базой данных Azure SQL."
keywords: "задание sqoop"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Узнайте, как toorun HDInsight .NET SDK toouse Sqoop заданий в HDInsight tooimport и экспорт между кластер HDInsight и база данных Azure SQL или база данных SQL Server.

> [!NOTE]
> в этой статье инструкциям Hello может использоваться с либо Windows или Linux HDInsight кластера; Однако эти действия, будет работать только с клиента Windows. Используйте выбора вкладки hello на hello верхней части этой статьи toochoose других методов.
> 
> 

### <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:

* **Кластер Hadoop в HDInsight**. Ознакомьтесь с разделом [Создание кластера и базы данных SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Использование Sqoop в кластерах HDInsight с помощью пакета SDK для .NET
Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET. В этом разделе создайте таблицы C# консольного приложения tooexport hello hivesampletable toohello базы данных SQL, созданный ранее в этом учебнике.

## <a name="submit-a-sqoop-job"></a>Отправка задания Sqoop

1. Создайте в Visual Studio консольное приложение C#.
2. Запустите следующий пакет hello tooimport команды Nuget hello из hello консоль диспетчера пакетов Visual Studio.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Используйте следующий код в файле Program.cs hello hello.
   
        using System.Collections.Generic;
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
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. Нажмите клавишу **F5** toorun hello программы. 

## <a name="limitations"></a>Ограничения
* Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.
* Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переход при выполнении вставки, Sqoop выполняет вставку нескольких вместо Пакетная обработка операций вставки hello.

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы узнали, как toouse Sqoop. toolearn более, см.:

* [Использование Oozie с HDInsight](hdinsight-use-oozie.md): используйте действие Sqoop в рабочем процессе Oozie.
* [Анализ данных задержки рейсов, с помощью HDInsight](hdinsight-analyze-flight-delay-data.md): используйте Hive рейса tooanalyze задержка данных, а затем использовать базы данных Azure SQL tooan Sqoop tooexport данных.
* [Отправка данных tooHDInsight](hdinsight-upload-data.md): найти другие методы для отправки данных tooHDInsight/Azure BLOB-объекта хранилища.

