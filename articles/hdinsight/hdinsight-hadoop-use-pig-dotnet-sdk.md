---
title: "Выполнение заданий Apache Pig с помощью пакета SDK для .NET для Hadoop в Azure HDInsight | Документы Майкрософт"
description: "Информация об использовании пакета SDK для .NET для Hadoop для отправки заданий Pig в Hadoop в HDInsight."
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
ms.openlocfilehash: e40d152821b36852c447d5a3adfd39114edbbace
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="run-pig-jobs-using-the-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="f05aa-103">Выполнение заданий Pig с помощью пакета SDK для .NET для Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f05aa-103">Run Pig jobs using the .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="f05aa-104">Узнайте, как использовать пакет SDK для .NET для Hadoop с целью отправки заданий Apache Pig в Hadoop в Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f05aa-104">Learn how to use the .NET SDK for Hadoop to submit Apache Pig jobs to Hadoop on Azure HDInsight.</span></span>

<span data-ttu-id="f05aa-105">Пакет SDK для HDInsight .NET предоставляет клиентские библиотеки .NET, которые упрощают работу с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="f05aa-105">The HDInsight .NET SDK provides .NET client libraries that makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="f05aa-106">Pig позволяет создавать операции MapReduce путем моделирования ряда преобразований данных.</span><span class="sxs-lookup"><span data-stu-id="f05aa-106">Pig allows you to create MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="f05aa-107">В этом документе вы узнаете, как отправлять задания Pig в кластер HDInsight с помощью базового приложения C#.</span><span class="sxs-lookup"><span data-stu-id="f05aa-107">In this document, you learn how to use a basic C# application to submit a Pig job to an HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f05aa-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f05aa-108">Prerequisites</span></span>

<span data-ttu-id="f05aa-109">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="f05aa-109">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="f05aa-110">Кластер Azure HDInsight (Hadoop в HDInsight) (на платформе Windows или Linux).</span><span class="sxs-lookup"><span data-stu-id="f05aa-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f05aa-111">Linux — единственная операционная система, используемая для работы с HDInsight 3.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f05aa-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f05aa-112">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f05aa-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="f05aa-113">Visual Studio 2012, 2013, 2015 или 2017.</span><span class="sxs-lookup"><span data-stu-id="f05aa-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="f05aa-114">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="f05aa-114">Create the application</span></span>

<span data-ttu-id="f05aa-115">Пакет SDK для HDInsight .NET содержит клиентские библиотеки .NET, которые упрощают работу с кластерами HDInsight из .NET.</span><span class="sxs-lookup"><span data-stu-id="f05aa-115">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="f05aa-116">В Visual Studio откройте меню **Файл** и выберите **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="f05aa-116">From the **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="f05aa-117">Для нового проекта введите или выберите следующие значения.</span><span class="sxs-lookup"><span data-stu-id="f05aa-117">For the new project, type or select the following values:</span></span>

   | <span data-ttu-id="f05aa-118">Свойство</span><span class="sxs-lookup"><span data-stu-id="f05aa-118">Property</span></span> | <span data-ttu-id="f05aa-119">Значение</span><span class="sxs-lookup"><span data-stu-id="f05aa-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="f05aa-120">Категория</span><span class="sxs-lookup"><span data-stu-id="f05aa-120">Category</span></span> | <span data-ttu-id="f05aa-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="f05aa-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="f05aa-122">Шаблон</span><span class="sxs-lookup"><span data-stu-id="f05aa-122">Template</span></span> | <span data-ttu-id="f05aa-123">Консольное приложение</span><span class="sxs-lookup"><span data-stu-id="f05aa-123">Console Application</span></span> |
   | <span data-ttu-id="f05aa-124">Имя</span><span class="sxs-lookup"><span data-stu-id="f05aa-124">Name</span></span> | <span data-ttu-id="f05aa-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="f05aa-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="f05aa-126">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="f05aa-126">Click **OK** to create the project.</span></span>

4. <span data-ttu-id="f05aa-127">В меню **Сервис** выберите пункт **Диспетчер пакетов библиотеки** или **Диспетчер пакетов Nuget**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="f05aa-127">From the **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="f05aa-128">Чтобы установить пакеты SDK для .NET, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f05aa-128">To install the .NET SDK packages, use the following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="f05aa-129">В обозревателе решений дважды щелкните **Program.cs** , чтобы открыть файл.</span><span class="sxs-lookup"><span data-stu-id="f05aa-129">From Solution Explorer, double-click **Program.cs** to open it.</span></span> <span data-ttu-id="f05aa-130">Замените имеющийся код следующим.</span><span class="sxs-lookup"><span data-stu-id="f05aa-130">Replace the existing code with the following.</span></span>

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
                System.Console.WriteLine("The application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER to continue ...");
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

                System.Console.WriteLine("Submitting the Pig job to the cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that the response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating the response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="f05aa-131">Чтобы запустить приложение, нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="f05aa-131">To start the application, press **F5**.</span></span>

8. <span data-ttu-id="f05aa-132">Чтобы завершить работу приложения, нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="f05aa-132">To exit the application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="f05aa-133">Сводка</span><span class="sxs-lookup"><span data-stu-id="f05aa-133">Summary</span></span>

<span data-ttu-id="f05aa-134">Как вы видите, пакет SDK для .NET для Hadoop позволяет создавать приложения .NET, которые будут отправлять задания Pig в кластер HDInsight и отслеживать состояние задания.</span><span class="sxs-lookup"><span data-stu-id="f05aa-134">As you can see, the .NET SDK for Hadoop allows you to create .NET applications that submit Pig jobs to an HDInsight cluster, and monitor the job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f05aa-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f05aa-135">Next steps</span></span>

<span data-ttu-id="f05aa-136">Сведения о Pig в HDInsight см. в разделе [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="f05aa-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="f05aa-137">Дополнительные сведения об использовании Hadoop в HDInsight см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="f05aa-137">For more information on using Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="f05aa-138">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f05aa-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f05aa-139">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="f05aa-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
