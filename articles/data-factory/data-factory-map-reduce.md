---
title: "aaaInvoke программу MapReduce из фабрики данных Azure"
description: "Узнайте, как кластер tooprocess данных путем запуска на Azure HDInsight программ MapReduce из фабрики данных Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="a9160-103">Вызов программы MapReduce из фабрики данных</span><span class="sxs-lookup"><span data-stu-id="a9160-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="a9160-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="a9160-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="a9160-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="a9160-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="a9160-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="a9160-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="a9160-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="a9160-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="a9160-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="a9160-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="a9160-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a9160-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="a9160-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a9160-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="a9160-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="a9160-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="a9160-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a9160-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="a9160-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="a9160-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="a9160-114">Действие MapReduce в HDInsight в фабрике данных Hello [конвейера](data-factory-create-pipelines.md) выполняет программ MapReduce, на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) кластера HDInsight под управлением Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="a9160-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a9160-115">Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.</span><span class="sxs-lookup"><span data-stu-id="a9160-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="a9160-116">Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a9160-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="a9160-117">Введение</span><span class="sxs-lookup"><span data-stu-id="a9160-117">Introduction</span></span>
<span data-ttu-id="a9160-118">Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб.</span><span class="sxs-lookup"><span data-stu-id="a9160-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="a9160-119">В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки.</span><span class="sxs-lookup"><span data-stu-id="a9160-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="a9160-120">В этой статье описывает использование hello действие MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9160-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="a9160-121">Дополнительную информацию о выполнении сценариев Pig и Hive в кластере HDInsight на основе Windows или Linux из конвейера с помощью действий Pig и Hive в HDInsight см. в статьях [Действие Pig](data-factory-pig-activity.md) и [Действие Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a9160-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="a9160-122">JSON для действия MapReduce в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9160-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="a9160-123">В hello определение JSON для hello действие HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a9160-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="a9160-124">Набор hello **тип** из hello **действия** слишком**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a9160-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="a9160-125">Укажите имя hello hello класса для **className** свойство.</span><span class="sxs-lookup"><span data-stu-id="a9160-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="a9160-126">Укажите hello путь toohello JAR-файл с именем файла hello для **jarFilePath** свойство.</span><span class="sxs-lookup"><span data-stu-id="a9160-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="a9160-127">Укажите hello связаны службы, которая ссылается toohello хранилища больших двоичных объектов, содержащий hello JAR-файл для **jarLinkedService** свойство.</span><span class="sxs-lookup"><span data-stu-id="a9160-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="a9160-128">Укажите необходимые аргументы для программы MapReduce hello в hello **аргументы** раздела.</span><span class="sxs-lookup"><span data-stu-id="a9160-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="a9160-129">Во время выполнения, появится несколько дополнительных аргументов (например: mapreduce.job.tags) на основе инфраструктуры MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="a9160-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="a9160-130">toodifferentiate аргументов с аргументами MapReduce hello, рассмотрите использование параметра и значение в качестве аргументов, как показано в следующий пример hello (- s,--входных данных, — т. д., выходные данные будут сразу следуют значениями параметров).</span><span class="sxs-lookup"><span data-stu-id="a9160-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="a9160-131">Действие MapReduce в HDInsight toorun hello можно использовать любой файл jar MapReduce в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9160-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="a9160-132">Следующий пример определения JSON конвейера, hello действие HDInsight — hello настроены toorun Mahout JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="a9160-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="a9160-133">Пример на GitHub</span><span class="sxs-lookup"><span data-stu-id="a9160-133">Sample on GitHub</span></span>
<span data-ttu-id="a9160-134">Вы можете загрузить пример использования hello действие MapReduce в HDInsight из: [фабрики образцы данных на сайте GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="a9160-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="a9160-135">Запуск программы Статистика hello</span><span class="sxs-lookup"><span data-stu-id="a9160-135">Running hello Word Count program</span></span>
<span data-ttu-id="a9160-136">конвейер Hello в этом примере запускается hello Статистика Map/Reduce программы в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9160-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="a9160-137">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="a9160-137">Linked Services</span></span>
<span data-ttu-id="a9160-138">Сначала необходимо создать hello toolink связанной службы хранилища Azure, используемой фабрики данных Azure toohello кластера Azure HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="a9160-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="a9160-139">Если вы скопируйте и вставьте следующий код hello, не забудьте tooreplace **имя учетной записи** и **ключ учетной записи** с именем hello и ключ хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a9160-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="a9160-140">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a9160-140">Azure Storage linked service</span></span>

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="a9160-141">Связанная служба Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9160-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="a9160-142">Создайте toolink связанной службы фабрики данных Azure toohello кластера Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9160-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="a9160-143">Если вы скопируйте и вставьте следующий код hello, замените **имя кластера HDInsight** с именем hello кластер HDInsight и изменение значения имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="a9160-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="a9160-144">НАБОРЫ ДАННЫХ</span><span class="sxs-lookup"><span data-stu-id="a9160-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="a9160-145">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="a9160-145">Output dataset</span></span>
<span data-ttu-id="a9160-146">конвейер Hello в этом примере не принимает входные данные.</span><span class="sxs-lookup"><span data-stu-id="a9160-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="a9160-147">Необходимо указать выходной набор данных для hello действие MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9160-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="a9160-148">Этот набор данных — просто пустой набор данных, необходимые toodrive hello конвейера расписание.</span><span class="sxs-lookup"><span data-stu-id="a9160-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="a9160-149">Конвейер</span><span class="sxs-lookup"><span data-stu-id="a9160-149">Pipeline</span></span>
<span data-ttu-id="a9160-150">конвейер Hello в этом примере имеется только одно действие, которое относится к типу: HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="a9160-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="a9160-151">Ниже приведены некоторые важные свойства hello в hello JSON.</span><span class="sxs-lookup"><span data-stu-id="a9160-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="a9160-152">Свойство</span><span class="sxs-lookup"><span data-stu-id="a9160-152">Property</span></span> | <span data-ttu-id="a9160-153">Примечания</span><span class="sxs-lookup"><span data-stu-id="a9160-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="a9160-154">type</span><span class="sxs-lookup"><span data-stu-id="a9160-154">type</span></span> |<span data-ttu-id="a9160-155">Hello тип должен быть установлен слишком**HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="a9160-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="a9160-156">className</span><span class="sxs-lookup"><span data-stu-id="a9160-156">className</span></span> |<span data-ttu-id="a9160-157">Имя класса hello: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="a9160-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="a9160-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="a9160-158">jarFilePath</span></span> |<span data-ttu-id="a9160-159">Путь toohello jar-файл содержит класс hello.</span><span class="sxs-lookup"><span data-stu-id="a9160-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="a9160-160">Если вы скопируйте и вставьте следующий код hello, не забывайте toochange hello имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="a9160-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="a9160-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="a9160-161">jarLinkedService</span></span> |<span data-ttu-id="a9160-162">Связанная служба, которая содержит hello jar-файл хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a9160-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="a9160-163">Эта связанная служба ссылается toohello хранилища, связанного с кластером HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="a9160-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="a9160-164">arguments</span><span class="sxs-lookup"><span data-stu-id="a9160-164">arguments</span></span> |<span data-ttu-id="a9160-165">Программа Hello wordcount принимает два аргумента, входным и выходным.</span><span class="sxs-lookup"><span data-stu-id="a9160-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="a9160-166">Hello входной файл является файлом davinci.txt hello.</span><span class="sxs-lookup"><span data-stu-id="a9160-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="a9160-167">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="a9160-167">frequency/interval</span></span> |<span data-ttu-id="a9160-168">значения этих свойств Hello соответствует hello выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="a9160-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="a9160-169">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="a9160-169">linkedServiceName</span></span> |<span data-ttu-id="a9160-170">ссылается toohello связанной службы HDInsight, был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="a9160-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="a9160-171">Запуск программ Spark</span><span class="sxs-lookup"><span data-stu-id="a9160-171">Run Spark programs</span></span>
<span data-ttu-id="a9160-172">Можно использовать программы Spark toorun действие MapReduce в кластере HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="a9160-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="a9160-173">Дополнительные сведения см. в разделе [Вызов программ Spark из фабрики данных](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="a9160-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="a9160-174">См. также</span><span class="sxs-lookup"><span data-stu-id="a9160-174">See Also</span></span>
* [<span data-ttu-id="a9160-175">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="a9160-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="a9160-176">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="a9160-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="a9160-177">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="a9160-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="a9160-178">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="a9160-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="a9160-179">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="a9160-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

