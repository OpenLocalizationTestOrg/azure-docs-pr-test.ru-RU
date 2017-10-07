---
title: "aaaTransform данные, используя действие потоковой передачи Hadoop - Azure | Документы Microsoft"
description: "Дополнительные сведения об использовании hello действие потоковой передачи Hadoop данных tootransform фабрики данных Azure путем запуска программ потоковой передачи Hadoop на запросу или ваш собственный кластер HDInsight."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="26386-103">Преобразование данных с помощью действия потоковой передачи Hadoop в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="26386-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="26386-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="26386-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="26386-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="26386-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="26386-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="26386-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="26386-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="26386-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="26386-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="26386-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="26386-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="26386-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="26386-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="26386-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="26386-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="26386-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="26386-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="26386-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="26386-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="26386-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="26386-114">Можно использовать hello HDInsightStreamingActivity действия вызова задания потоковой передачи Hadoop из конвейера фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="26386-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="26386-115">Hello следующем фрагменте JSON показан синтаксис hello использования hello HDInsightStreamingActivity в файле JSON конвейера.</span><span class="sxs-lookup"><span data-stu-id="26386-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="26386-116">Hello действие потоковой передачи HDInsight в фабрике данных [конвейера](data-factory-create-pipelines.md) выполняет программ потоковой передачи Hadoop на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight под управлением Windows и Linux кластер.</span><span class="sxs-lookup"><span data-stu-id="26386-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="26386-117">Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.</span><span class="sxs-lookup"><span data-stu-id="26386-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="26386-118">Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье.</span><span class="sxs-lookup"><span data-stu-id="26386-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="26386-119">Образец JSON</span><span class="sxs-lookup"><span data-stu-id="26386-119">JSON sample</span></span>
<span data-ttu-id="26386-120">кластер HDInsight Hello автоматически заполняется пример программы (wc.exe и cat.exe) и данные (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="26386-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="26386-121">По умолчанию имя контейнера hello, используемой кластером HDInsight hello — hello имя самого кластера hello.</span><span class="sxs-lookup"><span data-stu-id="26386-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="26386-122">Например если myhdicluster имя кластера, имя связанный контейнер больших двоичных объектов hello будет myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="26386-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="26386-123">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="26386-123">Note hello following points:</span></span>

1. <span data-ttu-id="26386-124">Набор hello **linkedServiceName** toohello имя hello связанной службы, которая указывает tooyour кластера HDInsight, на какие hello потоковой передачи mapreduce задание запускается.</span><span class="sxs-lookup"><span data-stu-id="26386-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="26386-125">Задайте тип hello hello действия слишком**HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="26386-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="26386-126">Для hello **сопоставления** свойство, укажите имя исполняемого файла модуля сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="26386-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="26386-127">В примере hello cat.exe является исполняемого файла модуля сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="26386-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="26386-128">Для hello **редуктора** свойство, укажите имя исполняемого файла редуктора hello.</span><span class="sxs-lookup"><span data-stu-id="26386-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="26386-129">В примере hello wc.exe — исполняемого файла редуктора hello.</span><span class="sxs-lookup"><span data-stu-id="26386-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="26386-130">Для hello **ввода** свойство type, укажите hello входного файла (в том числе расположение hello) для сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="26386-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="26386-131">В примере hello: «wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt»: adfsample — контейнер больших двоичных объектов hello, пример/data/Gutenberg — папка hello и davinci.txt — hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="26386-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="26386-132">Для hello **вывода** свойство type, укажите hello выходного файла (в том числе расположение hello) для hello редуктора.</span><span class="sxs-lookup"><span data-stu-id="26386-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="26386-133">выходные данные задания потоковой передачи Hadoop hello Hello записывается toohello расположение, заданное для этого свойства.</span><span class="sxs-lookup"><span data-stu-id="26386-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="26386-134">В hello **filePaths** статьи, укажите пути hello для исполняемых файлов сопоставления и редуктора hello.</span><span class="sxs-lookup"><span data-stu-id="26386-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="26386-135">В примере hello: «adfsample/example/apps/wc.exe» adfsample — hello контейнер больших двоичных объектов, example/apps — папка hello и wc.exe — hello исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="26386-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="26386-136">Для hello **fileLinkedService** свойство, укажите hello связанной службы, которая представляет hello хранилища Azure, содержащей hello файлы, указанные в разделе filePaths hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="26386-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="26386-137">Для hello **аргументы** свойство, задайте аргументы hello для потоковой передачи задания hello.</span><span class="sxs-lookup"><span data-stu-id="26386-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="26386-138">Hello **getDebugInfo** свойство — это необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="26386-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="26386-139">Если он имеет значение tooFailure, hello журналы будут загружены только при сбое.</span><span class="sxs-lookup"><span data-stu-id="26386-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="26386-140">Если он имеет значение tooAlways, журналы, загружаются всегда независимо от состояния выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="26386-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="26386-141">Как показано в примере hello, можно указать выходной набор данных для hello действие потоковой передачи Hadoop для hello **выводит** свойство.</span><span class="sxs-lookup"><span data-stu-id="26386-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="26386-142">Этот набор данных — просто пустой набор данных, необходимые toodrive hello конвейера расписание.</span><span class="sxs-lookup"><span data-stu-id="26386-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="26386-143">Нет необходимости toospecify любого входного набора данных для действия "hello" для hello **входов** свойство.</span><span class="sxs-lookup"><span data-stu-id="26386-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="26386-144">Пример</span><span class="sxs-lookup"><span data-stu-id="26386-144">Example</span></span>
<span data-ttu-id="26386-145">конвейер Hello в этом пошаговом руководстве hello Статистика потоковой передачи Map/Reduce программа будет запущена на кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26386-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="26386-146">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="26386-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="26386-147">Связанная служба хранения Azure</span><span class="sxs-lookup"><span data-stu-id="26386-147">Azure Storage linked service</span></span>
<span data-ttu-id="26386-148">Сначала необходимо создать hello toolink связанной службы хранилища Azure, используемой фабрики данных Azure toohello кластера Azure HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="26386-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="26386-149">Если вы скопируйте и вставьте следующий код hello, не забудьте tooreplace учетной записи имя и учетную запись с именем hello и ключ хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="26386-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="26386-150">Связанная служба Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="26386-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="26386-151">Создайте toolink связанной службы фабрики данных Azure toohello кластера Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26386-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="26386-152">Если вы скопируйте и вставьте следующий код hello, замените имя кластера HDInsight hello имя кластера HDInsight и измените значения имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="26386-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="26386-153">НАБОРЫ ДАННЫХ</span><span class="sxs-lookup"><span data-stu-id="26386-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="26386-154">Выходной набор данных</span><span class="sxs-lookup"><span data-stu-id="26386-154">Output dataset</span></span>
<span data-ttu-id="26386-155">конвейер Hello в этом примере не принимает входные данные.</span><span class="sxs-lookup"><span data-stu-id="26386-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="26386-156">Необходимо указать выходной набор данных для hello действие потоковой передачи HDInsight.</span><span class="sxs-lookup"><span data-stu-id="26386-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="26386-157">Этот набор данных — просто пустой набор данных, необходимые toodrive hello конвейера расписание.</span><span class="sxs-lookup"><span data-stu-id="26386-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="26386-158">Конвейер</span><span class="sxs-lookup"><span data-stu-id="26386-158">Pipeline</span></span>
<span data-ttu-id="26386-159">конвейер Hello в этом примере имеется только одно действие, которое относится к типу: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="26386-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="26386-160">кластер HDInsight Hello автоматически заполняется пример программы (wc.exe и cat.exe) и данные (davinci.txt).</span><span class="sxs-lookup"><span data-stu-id="26386-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="26386-161">По умолчанию имя контейнера hello, используемой кластером HDInsight hello — hello имя самого кластера hello.</span><span class="sxs-lookup"><span data-stu-id="26386-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="26386-162">Например если myhdicluster имя кластера, имя связанный контейнер больших двоичных объектов hello будет myhdicluster.</span><span class="sxs-lookup"><span data-stu-id="26386-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="26386-163">См. также</span><span class="sxs-lookup"><span data-stu-id="26386-163">See Also</span></span>
* [<span data-ttu-id="26386-164">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="26386-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="26386-165">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="26386-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="26386-166">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="26386-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="26386-167">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="26386-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="26386-168">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="26386-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

