---
title: "Вызов программы MapReduce из фабрики данных Azure"
description: "Узнайте, как обрабатывать данные путем выполнения программ MapReduce в кластере Azure HDInsight из фабрики данных Azure."
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
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="a118a-103">Вызов программы MapReduce из фабрики данных</span><span class="sxs-lookup"><span data-stu-id="a118a-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="a118a-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="a118a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="a118a-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="a118a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="a118a-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="a118a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="a118a-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="a118a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="a118a-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="a118a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="a118a-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a118a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="a118a-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="a118a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="a118a-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="a118a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="a118a-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a118a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="a118a-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="a118a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="a118a-114">Действие MapReduce HDInsight в [конвейере](data-factory-create-pipelines.md) фабрики данных выполняет программы MapReduce для [вашего собственного](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) кластера HDInsight или кластера HDInsight [по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="a118a-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="a118a-115">Данная статья основана на материалах статьи о [действиях преобразования данных](data-factory-data-transformation-activities.md) , в которой приведен общий обзор преобразования данных и список поддерживаемых действий преобразования.</span><span class="sxs-lookup"><span data-stu-id="a118a-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="a118a-116">Если вы не знакомы с фабрикой данных Azure, ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md) и [Руководство. Создание первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md) перед ознакомлением с этой статьей.</span><span class="sxs-lookup"><span data-stu-id="a118a-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="a118a-117">Введение</span><span class="sxs-lookup"><span data-stu-id="a118a-117">Introduction</span></span>
<span data-ttu-id="a118a-118">Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб.</span><span class="sxs-lookup"><span data-stu-id="a118a-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="a118a-119">В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки.</span><span class="sxs-lookup"><span data-stu-id="a118a-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="a118a-120">В этой статье описывается использование действия MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a118a-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="a118a-121">Дополнительную информацию о выполнении сценариев Pig и Hive в кластере HDInsight на основе Windows или Linux из конвейера с помощью действий Pig и Hive в HDInsight см. в статьях [Действие Pig](data-factory-pig-activity.md) и [Действие Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a118a-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="a118a-122">JSON для действия MapReduce в HDInsight</span><span class="sxs-lookup"><span data-stu-id="a118a-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="a118a-123">В определении JSON для действия HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a118a-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="a118a-124">В поле **тип** для **действия** задайте значение **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a118a-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="a118a-125">Укажите имя класса для свойства **className** .</span><span class="sxs-lookup"><span data-stu-id="a118a-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="a118a-126">Укажите путь к JAR-файлу, включив в него имя файла для свойства **jarFilePath** .</span><span class="sxs-lookup"><span data-stu-id="a118a-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="a118a-127">Укажите связанную службу, которая обращается к хранилищу больших двоичных объектов Azure, содержащему JAR-файл для свойства **jarLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="a118a-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="a118a-128">Укажите необходимые аргументы для программы MapReduce в разделе **аргументы**.</span><span class="sxs-lookup"><span data-stu-id="a118a-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="a118a-129">Во время выполнения вы увидите несколько дополнительных аргументов (например, mapreduce.job.tags) платформы MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a118a-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="a118a-130">Чтобы отличать свои аргументы от аргументов MapReduce, вы можете использовать параметр и значение в качестве аргументов, как показано в следующем примере (-s, --input, --output и т. д — параметры, за которыми сразу следуют их значения).</span><span class="sxs-lookup"><span data-stu-id="a118a-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="a118a-131">С помощью действия MapReduce можно выполнить JAR-файл MapReduce в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a118a-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="a118a-132">В приведенном ниже образце определения конвейера JSON действие HDInsight настроено на запуск JAR-файла Mahout.</span><span class="sxs-lookup"><span data-stu-id="a118a-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="a118a-133">Пример на GitHub</span><span class="sxs-lookup"><span data-stu-id="a118a-133">Sample on GitHub</span></span>
<span data-ttu-id="a118a-134">Вы можете скачать пример использования действия MapReduce в HDInsight на странице [примеров фабрики данных на сайте GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span><span class="sxs-lookup"><span data-stu-id="a118a-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="a118a-135">Выполнение программы подсчета слов</span><span class="sxs-lookup"><span data-stu-id="a118a-135">Running the Word Count program</span></span>
<span data-ttu-id="a118a-136">Конвейер в этом примере запускает в кластере Azure HDInsight программу подсчета слов MapReduce.</span><span class="sxs-lookup"><span data-stu-id="a118a-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="a118a-137">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="a118a-137">Linked Services</span></span>
<span data-ttu-id="a118a-138">Сначала необходимо создать связанную службу для связи службы хранилища Azure, используемой в кластере Azure HDInsight, с фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a118a-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="a118a-139">При копировании и вставке следующего кода не забудьте заменить **имя** и **ключ учетной записи** именем и ключом хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a118a-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="a118a-140">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a118a-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="a118a-141">Связанная служба Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a118a-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="a118a-142">Далее необходимо создать связанную службу для связи кластера Azure HDInsight с фабрикой данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a118a-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="a118a-143">При копировании и вставке следующего кода не забудьте заменить **имя кластера HDInsight** на имя вашего кластера HDInsight и изменить значения имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="a118a-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="a118a-144">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="a118a-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="a118a-145">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="a118a-145">Output dataset</span></span>
<span data-ttu-id="a118a-146">Конвейер в этом примере не принимает никаких входных данных.</span><span class="sxs-lookup"><span data-stu-id="a118a-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="a118a-147">Следует указать выходной набор данных для действия MapReduce в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a118a-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="a118a-148">Это просто фиктивный набор данных, необходимый для соблюдения расписания конвейера.</span><span class="sxs-lookup"><span data-stu-id="a118a-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="a118a-149">Конвейер</span><span class="sxs-lookup"><span data-stu-id="a118a-149">Pipeline</span></span>
<span data-ttu-id="a118a-150">Конвейер в этом примере имеет только одно действие с типом HDInsightMapReduce.</span><span class="sxs-lookup"><span data-stu-id="a118a-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="a118a-151">Ниже приведены некоторые важные свойства в JSON.</span><span class="sxs-lookup"><span data-stu-id="a118a-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="a118a-152">Свойство</span><span class="sxs-lookup"><span data-stu-id="a118a-152">Property</span></span> | <span data-ttu-id="a118a-153">Примечания</span><span class="sxs-lookup"><span data-stu-id="a118a-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="a118a-154">type</span><span class="sxs-lookup"><span data-stu-id="a118a-154">type</span></span> |<span data-ttu-id="a118a-155">Должен быть задан тип **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="a118a-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="a118a-156">className</span><span class="sxs-lookup"><span data-stu-id="a118a-156">className</span></span> |<span data-ttu-id="a118a-157">Имя класса: **wordcount**</span><span class="sxs-lookup"><span data-stu-id="a118a-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="a118a-158">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="a118a-158">jarFilePath</span></span> |<span data-ttu-id="a118a-159">Путь к JAR-файлу, содержащему этот класс.</span><span class="sxs-lookup"><span data-stu-id="a118a-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="a118a-160">Если вы копируете и вставляете приведенный код, не забудьте изменить имя кластера.</span><span class="sxs-lookup"><span data-stu-id="a118a-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="a118a-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="a118a-161">jarLinkedService</span></span> |<span data-ttu-id="a118a-162">Служба, связанная со службой хранилища Azure, содержащая JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="a118a-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="a118a-163">Эта связанная служба ссылается на хранилище, связанное с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a118a-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="a118a-164">arguments</span><span class="sxs-lookup"><span data-stu-id="a118a-164">arguments</span></span> |<span data-ttu-id="a118a-165">Программа подсчета слов принимает два аргумента, входной и выходной.</span><span class="sxs-lookup"><span data-stu-id="a118a-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="a118a-166">Входной файл — davinci.txt.</span><span class="sxs-lookup"><span data-stu-id="a118a-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="a118a-167">frequency и interval</span><span class="sxs-lookup"><span data-stu-id="a118a-167">frequency/interval</span></span> |<span data-ttu-id="a118a-168">Значения этих свойств соответствуют результирующему набору данных.</span><span class="sxs-lookup"><span data-stu-id="a118a-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="a118a-169">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="a118a-169">linkedServiceName</span></span> |<span data-ttu-id="a118a-170">Указывает связанную службу HDInsight, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="a118a-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="a118a-171">Запуск программ Spark</span><span class="sxs-lookup"><span data-stu-id="a118a-171">Run Spark programs</span></span>
<span data-ttu-id="a118a-172">Действие MapReduce можно использовать для запуска программ Spark в кластере HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="a118a-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="a118a-173">Дополнительные сведения см. в разделе [Вызов программ Spark из фабрики данных](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="a118a-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="a118a-174">См. также</span><span class="sxs-lookup"><span data-stu-id="a118a-174">See Also</span></span>
* [<span data-ttu-id="a118a-175">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="a118a-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="a118a-176">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="a118a-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="a118a-177">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="a118a-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="a118a-178">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="a118a-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="a118a-179">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="a118a-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

