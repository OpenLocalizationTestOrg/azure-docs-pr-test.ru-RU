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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Запуск заданий Pig, с помощью hello .NET SDK для Hadoop в HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Узнайте, как toouse hello .NET SDK для toosubmit Hadoop Apache Pig заданий tooHadoop на Azure HDInsight.

Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, делает его проще toowork с кластерами HDInsight из .NET. Pig позволяет toocreate MapReduce операций путем моделирования ряд преобразования данных. В этом документе вы узнаете, как приложение toouse основные C# toosubmit Pig задания tooan кластера HDInsight.

## <a name="prerequisites"></a>Предварительные требования

в этой статье инструкциям toocomplete hello, необходимо следующее hello.

* Кластер Azure HDInsight (Hadoop в HDInsight) (на платформе Windows или Linux).

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012, 2013, 2015 или 2017.

## <a name="create-hello-application"></a>Создание приложения hello

Hello HDInsight .NET SDK предоставляет клиентские библиотеки .NET, что делает его проще toowork с кластерами HDInsight из .NET.

1. Из hello **файл** в Visual Studio, выберите пункт меню **New** , а затем выберите **проекта**.

2. Новый проект hello типа или выберите hello следующие значения:

   | Свойство | Значение |
   | ------ | ------ |
   | Категория | Templates/Visual C#/Windows |
   | Шаблон | Консольное приложение |
   | Имя | SubmitPigJob |

3. Нажмите кнопку **ОК** toocreate hello проекта.

4. Из hello **средства** последовательно выберите пункты **диспетчер пакетов библиотеки** или **диспетчера пакетов Nuget**и выберите **консоль диспетчера пакетов**.

5. пакеты .NET SDK tooinstall hello, используйте hello следующую команду:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. В обозревателе решений дважды щелкните **Program.cs** tooopen его. Замените существующий код hello hello следующее.

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

7. приложение hello toostart, нажмите клавишу **F5**.

8. приложение hello tooexit, нажмите клавишу **ввод**.

## <a name="summary"></a>Сводка

Как видите, hello .NET SDK для Hadoop позволяет приложениям .NET toocreate отправлять кластера HDInsight tooan задания Pig и отслеживать состояние задания hello.

## <a name="next-steps"></a>Дальнейшие действия

Сведения о Pig в HDInsight см. в разделе [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).

Дополнительные сведения об использовании Hadoop в HDInsight см. в разделе hello следующие документы:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
