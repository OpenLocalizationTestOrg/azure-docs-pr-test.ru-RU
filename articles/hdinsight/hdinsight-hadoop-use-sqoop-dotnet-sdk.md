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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="33fca-104">Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="33fca-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="33fca-105">Узнайте, как toorun HDInsight .NET SDK toouse Sqoop заданий в HDInsight tooimport и экспорт между кластер HDInsight и база данных Azure SQL или база данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="33fca-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="33fca-106">в этой статье инструкциям Hello может использоваться с либо Windows или Linux HDInsight кластера; Однако эти действия, будет работать только с клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="33fca-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="33fca-107">Используйте выбора вкладки hello на hello верхней части этой статьи toochoose других методов.</span><span class="sxs-lookup"><span data-stu-id="33fca-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="33fca-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="33fca-108">Prerequisites</span></span>
<span data-ttu-id="33fca-109">Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="33fca-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="33fca-110">**Кластер Hadoop в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="33fca-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="33fca-111">Ознакомьтесь с разделом [Создание кластера и базы данных SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="33fca-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="33fca-112">Использование Sqoop в кластерах HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="33fca-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="33fca-113">Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="33fca-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="33fca-114">В этом разделе создайте таблицы C# консольного приложения tooexport hello hivesampletable toohello базы данных SQL, созданный ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="33fca-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="33fca-115">Отправка задания Sqoop</span><span class="sxs-lookup"><span data-stu-id="33fca-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="33fca-116">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="33fca-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="33fca-117">Запустите следующий пакет hello tooimport команды Nuget hello из hello консоль диспетчера пакетов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33fca-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="33fca-118">Используйте следующий код в файле Program.cs hello hello.</span><span class="sxs-lookup"><span data-stu-id="33fca-118">Use hello following code in hello Program.cs file:</span></span>
   
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
4. <span data-ttu-id="33fca-119">Нажмите клавишу **F5** toorun hello программы.</span><span class="sxs-lookup"><span data-stu-id="33fca-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="33fca-120">Ограничения</span><span class="sxs-lookup"><span data-stu-id="33fca-120">Limitations</span></span>
* <span data-ttu-id="33fca-121">Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="33fca-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="33fca-122">Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переход при выполнении вставки, Sqoop выполняет вставку нескольких вместо Пакетная обработка операций вставки hello.</span><span class="sxs-lookup"><span data-stu-id="33fca-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33fca-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33fca-123">Next steps</span></span>
<span data-ttu-id="33fca-124">Теперь вы узнали, как toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="33fca-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="33fca-125">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="33fca-125">toolearn more, see:</span></span>

* <span data-ttu-id="33fca-126">[Использование Oozie с HDInsight](hdinsight-use-oozie.md): используйте действие Sqoop в рабочем процессе Oozie.</span><span class="sxs-lookup"><span data-stu-id="33fca-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="33fca-127">[Анализ данных задержки рейсов, с помощью HDInsight](hdinsight-analyze-flight-delay-data.md): используйте Hive рейса tooanalyze задержка данных, а затем использовать базы данных Azure SQL tooan Sqoop tooexport данных.</span><span class="sxs-lookup"><span data-stu-id="33fca-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="33fca-128">[Отправка данных tooHDInsight](hdinsight-upload-data.md): найти другие методы для отправки данных tooHDInsight/Azure BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="33fca-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

