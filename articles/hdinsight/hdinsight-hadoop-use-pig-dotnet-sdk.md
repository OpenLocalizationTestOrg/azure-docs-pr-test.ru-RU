---
title: "aaaRun Apache Pig задания с помощью пакета SDK .NET для Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse hello .NET SDK для tooHadoop задания Pig toosubmit Hadoop в HDInsight."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="c3ee0-103">Запуск заданий Pig, с помощью hello .NET SDK для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3ee0-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="c3ee0-104">Узнайте, как toouse hello .NET SDK для toosubmit Hadoop Apache Pig заданий tooHadoop на Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="c3ee0-105">Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, делает его проще toowork с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="c3ee0-106">Pig позволяет toocreate MapReduce операций путем моделирования ряд преобразования данных.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="c3ee0-107">В этом документе вы узнаете, как приложение toouse основные C# toosubmit Pig задания tooan кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3ee0-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3ee0-108">Prerequisites</span></span>

<span data-ttu-id="c3ee0-109">в этой статье инструкциям toocomplete hello, необходимо следующее hello.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="c3ee0-110">Кластер Azure HDInsight (Hadoop в HDInsight) (на платформе Windows или Linux).</span><span class="sxs-lookup"><span data-stu-id="c3ee0-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c3ee0-111">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3ee0-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c3ee0-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c3ee0-113">Visual Studio 2012, 2013, 2015 или 2017.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="c3ee0-114">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="c3ee0-114">Create hello application</span></span>

<span data-ttu-id="c3ee0-115">Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="c3ee0-116">Из hello **файл** в Visual Studio, выберите пункт меню **New** , а затем выберите **проекта**.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="c3ee0-117">Новый проект hello типа или выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c3ee0-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="c3ee0-118">Свойство</span><span class="sxs-lookup"><span data-stu-id="c3ee0-118">Property</span></span> | <span data-ttu-id="c3ee0-119">Значение</span><span class="sxs-lookup"><span data-stu-id="c3ee0-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="c3ee0-120">Категория</span><span class="sxs-lookup"><span data-stu-id="c3ee0-120">Category</span></span> | <span data-ttu-id="c3ee0-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="c3ee0-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="c3ee0-122">Шаблон</span><span class="sxs-lookup"><span data-stu-id="c3ee0-122">Template</span></span> | <span data-ttu-id="c3ee0-123">Консольное приложение</span><span class="sxs-lookup"><span data-stu-id="c3ee0-123">Console Application</span></span> |
   | <span data-ttu-id="c3ee0-124">Имя</span><span class="sxs-lookup"><span data-stu-id="c3ee0-124">Name</span></span> | <span data-ttu-id="c3ee0-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="c3ee0-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="c3ee0-126">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="c3ee0-127">Из hello **средства** последовательно выберите пункты **диспетчер пакетов библиотеки** или **диспетчера пакетов Nuget**и выберите **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="c3ee0-128">пакеты .NET SDK tooinstall hello, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c3ee0-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="c3ee0-129">В обозревателе решений дважды щелкните **Program.cs** tooopen его.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="c3ee0-130">Замените существующий код hello hello следующее.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-130">Replace hello existing code with hello following.</span></span>

    ```csharp
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

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="c3ee0-131">приложение hello toostart, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="c3ee0-132">приложение hello tooexit, нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="c3ee0-133">Сводка</span><span class="sxs-lookup"><span data-stu-id="c3ee0-133">Summary</span></span>

<span data-ttu-id="c3ee0-134">Как видите, hello .NET SDK для Hadoop позволяет приложениям .NET toocreate отправлять кластера HDInsight tooan задания Pig и отслеживать состояние задания hello.</span><span class="sxs-lookup"><span data-stu-id="c3ee0-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ee0-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3ee0-135">Next steps</span></span>

<span data-ttu-id="c3ee0-136">Сведения о Pig в HDInsight см. в разделе [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="c3ee0-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="c3ee0-137">Дополнительные сведения об использовании Hadoop в HDInsight см. в разделе hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="c3ee0-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="c3ee0-138">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3ee0-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c3ee0-139">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3ee0-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
