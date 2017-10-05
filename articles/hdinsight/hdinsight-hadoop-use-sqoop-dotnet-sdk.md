---
title: "Выполнение заданий Sqoop с помощью .NET и HDInsight в Azure | Документы Майкрософт"
description: "Узнайте, как использовать пакет SDK HDInsight для .NET, чтобы выполнять импорт и экспорт Sqoop между кластером HDInsight и базой данных SQL Azure."
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="4b287-104">Выполнение заданий Sqoop с помощью пакета SDK для .NET для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="4b287-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="4b287-105">Узнайте, как использовать пакет SDK HDInsight для .NET для выполнения заданий Sqoop, осуществляющих импорт и экспорт между кластером HDInsight и базой данных SQL Azure или базой данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4b287-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="4b287-106">Действия, описанные в этой статье, можно использовать для кластера HDInsight под управлением Windows или Linux. Однако эти действия можно выполнять только из клиента Windows.</span><span class="sxs-lookup"><span data-stu-id="4b287-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="4b287-107">Используйте выбор вкладок в верхней части этой статьи, чтобы выбрать другие методы.</span><span class="sxs-lookup"><span data-stu-id="4b287-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="4b287-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4b287-108">Prerequisites</span></span>
<span data-ttu-id="4b287-109">Перед началом работы с этим руководством необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="4b287-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="4b287-110">**Кластер Hadoop в HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4b287-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="4b287-111">Ознакомьтесь с разделом [Создание кластера и базы данных SQL](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="4b287-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="4b287-112">Использование Sqoop в кластерах HDInsight с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="4b287-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="4b287-113">Пакет SDK для HDInsight .NET содержит клиентские библиотеки .NET, которые упрощают работу с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="4b287-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="4b287-114">В этом разделе вы создадите консольное приложение C# для экспорта hivesampletable в созданную ранее таблицу базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4b287-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="4b287-115">Отправка задания Sqoop</span><span class="sxs-lookup"><span data-stu-id="4b287-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="4b287-116">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="4b287-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="4b287-117">В Консоли диспетчера пакетов Visual Studio выполните следующую команду Nuget, чтобы импортировать пакет:</span><span class="sxs-lookup"><span data-stu-id="4b287-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="4b287-118">Используйте следующий код в файле Program.cs.</span><span class="sxs-lookup"><span data-stu-id="4b287-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="4b287-119">Нажмите клавишу **F5** для запуска программы.</span><span class="sxs-lookup"><span data-stu-id="4b287-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="4b287-120">Ограничения</span><span class="sxs-lookup"><span data-stu-id="4b287-120">Limitations</span></span>
* <span data-ttu-id="4b287-121">Массовый экспорт: при использовании HDInsight на основе Linux соединитель Sqoop, применяемый для экспорта данных в Microsoft SQL Server или базу данных SQL Azure, пока не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="4b287-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="4b287-122">Пакетная обработка: при использовании HDInsight на основе Linux, когда для вставок применяется параметр `-batch`, Sqoop выполняет несколько вставок вместо пакетной обработки операций вставки.</span><span class="sxs-lookup"><span data-stu-id="4b287-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b287-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4b287-123">Next steps</span></span>
<span data-ttu-id="4b287-124">Теперь вы узнали, как использовать Sqoop.</span><span class="sxs-lookup"><span data-stu-id="4b287-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="4b287-125">Дополнительные сведения см. на следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="4b287-125">To learn more, see:</span></span>

* <span data-ttu-id="4b287-126">[Использование Oozie с HDInsight](hdinsight-use-oozie.md): используйте действие Sqoop в рабочем процессе Oozie.</span><span class="sxs-lookup"><span data-stu-id="4b287-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="4b287-127">[Анализ данных о задержке рейсов с помощью HDInsight](hdinsight-analyze-flight-delay-data.md): используйте Hive для анализа данных о задержке рейсов, а затем используйте Sqoop для экспорта данных в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4b287-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="4b287-128">[Передача данных в HDInsight](hdinsight-upload-data.md): узнайте о других способах отправки данных в HDInsight и хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="4b287-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

