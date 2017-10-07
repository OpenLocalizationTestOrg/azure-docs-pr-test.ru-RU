---
title: "aaaTransform данных, с помощью действия Hive - Azure | Документы Microsoft"
description: "Дополнительные сведения об использовании hello действие Hive в запросы Hive toorun фабрики данных Azure в кластере HDInsight на запросу или свой собственный."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="6392a-103">Преобразование данных с помощью действия Hive в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="6392a-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="6392a-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="6392a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="6392a-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="6392a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="6392a-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="6392a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="6392a-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="6392a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="6392a-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="6392a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="6392a-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="6392a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="6392a-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="6392a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="6392a-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="6392a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="6392a-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6392a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="6392a-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="6392a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="6392a-114">Hello действие Hive в HDInsight в фабрике данных [конвейера](data-factory-create-pipelines.md) выполняет запросы Hive на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) кластера HDInsight под управлением Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="6392a-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="6392a-115">Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.</span><span class="sxs-lookup"><span data-stu-id="6392a-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="6392a-116">Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье.</span><span class="sxs-lookup"><span data-stu-id="6392a-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="6392a-117">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="6392a-117">Syntax</span></span>

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a><span data-ttu-id="6392a-118">Сведения о синтаксисе</span><span class="sxs-lookup"><span data-stu-id="6392a-118">Syntax details</span></span>
| <span data-ttu-id="6392a-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="6392a-119">Property</span></span> | <span data-ttu-id="6392a-120">Описание</span><span class="sxs-lookup"><span data-stu-id="6392a-120">Description</span></span> | <span data-ttu-id="6392a-121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6392a-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6392a-122">name</span><span class="sxs-lookup"><span data-stu-id="6392a-122">name</span></span> |<span data-ttu-id="6392a-123">Имя действия hello</span><span class="sxs-lookup"><span data-stu-id="6392a-123">Name of hello activity</span></span> |<span data-ttu-id="6392a-124">Да</span><span class="sxs-lookup"><span data-stu-id="6392a-124">Yes</span></span> |
| <span data-ttu-id="6392a-125">Описание</span><span class="sxs-lookup"><span data-stu-id="6392a-125">description</span></span> |<span data-ttu-id="6392a-126">Текст, описывающий, какое действие hello используется для</span><span class="sxs-lookup"><span data-stu-id="6392a-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="6392a-127">Нет</span><span class="sxs-lookup"><span data-stu-id="6392a-127">No</span></span> |
| <span data-ttu-id="6392a-128">type</span><span class="sxs-lookup"><span data-stu-id="6392a-128">type</span></span> |<span data-ttu-id="6392a-129">HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="6392a-129">HDinsightHive</span></span> |<span data-ttu-id="6392a-130">Да</span><span class="sxs-lookup"><span data-stu-id="6392a-130">Yes</span></span> |
| <span data-ttu-id="6392a-131">inputs</span><span class="sxs-lookup"><span data-stu-id="6392a-131">inputs</span></span> |<span data-ttu-id="6392a-132">Входные данные, используемые действием Hive hello</span><span class="sxs-lookup"><span data-stu-id="6392a-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="6392a-133">Нет</span><span class="sxs-lookup"><span data-stu-id="6392a-133">No</span></span> |
| <span data-ttu-id="6392a-134">outputs</span><span class="sxs-lookup"><span data-stu-id="6392a-134">outputs</span></span> |<span data-ttu-id="6392a-135">Выходные данные, полученные в результате действия Hive hello</span><span class="sxs-lookup"><span data-stu-id="6392a-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="6392a-136">Да</span><span class="sxs-lookup"><span data-stu-id="6392a-136">Yes</span></span> |
| <span data-ttu-id="6392a-137">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="6392a-137">linkedServiceName</span></span> |<span data-ttu-id="6392a-138">Кластер HDInsight toohello ссылка зарегистрирован как связанной службы в фабрике данных</span><span class="sxs-lookup"><span data-stu-id="6392a-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="6392a-139">Да</span><span class="sxs-lookup"><span data-stu-id="6392a-139">Yes</span></span> |
| <span data-ttu-id="6392a-140">script</span><span class="sxs-lookup"><span data-stu-id="6392a-140">script</span></span> |<span data-ttu-id="6392a-141">Укажите встроенного скрипта Hive hello</span><span class="sxs-lookup"><span data-stu-id="6392a-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="6392a-142">Нет</span><span class="sxs-lookup"><span data-stu-id="6392a-142">No</span></span> |
| <span data-ttu-id="6392a-143">script path</span><span class="sxs-lookup"><span data-stu-id="6392a-143">script path</span></span> |<span data-ttu-id="6392a-144">Хранилище hello Hive скрипт в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="6392a-145">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="6392a-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="6392a-146">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="6392a-146">Both cannot be used together.</span></span> <span data-ttu-id="6392a-147">Имя файла Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="6392a-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="6392a-148">Нет</span><span class="sxs-lookup"><span data-stu-id="6392a-148">No</span></span> |
| <span data-ttu-id="6392a-149">defines</span><span class="sxs-lookup"><span data-stu-id="6392a-149">defines</span></span> |<span data-ttu-id="6392a-150">Укажите параметры как пары "ключ значение" для ссылки на куст скрипте hello «hiveconf»</span><span class="sxs-lookup"><span data-stu-id="6392a-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="6392a-151">Нет</span><span class="sxs-lookup"><span data-stu-id="6392a-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="6392a-152">Пример</span><span class="sxs-lookup"><span data-stu-id="6392a-152">Example</span></span>
<span data-ttu-id="6392a-153">Давайте рассмотрим пример игры журналы аналитики, где требуется tooidentify hello времени, затраченного пользователями, игры, запускаемого по вашей компании.</span><span class="sxs-lookup"><span data-stu-id="6392a-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="6392a-154">Hello следующий журнал приведен пример игры журнала, который является запятая (`,`) разделены и содержит следующие поля — ProfileID, SessionStart, длительность, SrcIPAddress и GameType hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="6392a-155">Hello **скрипта Hive** tooprocess эти данные:</span><span class="sxs-lookup"><span data-stu-id="6392a-155">hello **Hive script** tooprocess this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="6392a-156">tooexecute этот куст сценария в конвейере фабрики данных, требуются следующие toodo hello</span><span class="sxs-lookup"><span data-stu-id="6392a-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="6392a-157">Создание tooregister связанной службы [собственные HDInsight вычислительный кластер](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или настроить [вычислительный кластер HDInsight по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="6392a-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="6392a-158">Назовем эту связанную службу HDInsightLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6392a-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="6392a-159">Создание [связанная служба](data-factory-azure-blob-connector.md) tooconfigure hello подключения tooAzure хранилища BLOB-данных размещение данных hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="6392a-160">Назовем эту связанную службу StorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6392a-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="6392a-161">Создание [наборы данных](data-factory-create-datasets.md) и toohello входных данных, а затем hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6392a-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="6392a-162">Давайте hello вызовов входной набор данных «HiveSampleIn» и hello выходной набор данных «HiveSampleOut»</span><span class="sxs-lookup"><span data-stu-id="6392a-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="6392a-163">Запрос Hive hello Копировать как файл tooAzure хранилища больших двоичных объектов, настроенную на шаге #2.</span><span class="sxs-lookup"><span data-stu-id="6392a-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="6392a-164">Если hello хранилища для размещения данных hello отличается от hello одно размещение этот файл запроса, создайте отдельный связанной службой хранилища Azure и tooit в действии hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="6392a-165">Используйте ** scriptPath ** hello путь toospecify toohive-файл запроса и **scriptLinkedService** toospecify hello хранилища Azure, содержащей файл скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6392a-166">Можно также предоставить с помощью hello встроенного скрипта Hive hello в определении действия hello **сценарий** свойство.</span><span class="sxs-lookup"><span data-stu-id="6392a-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="6392a-167">Не рекомендуется этот подход, а все специальные символы в скрипте hello в документе JSON hello необходимо экранировать toobe может причина отладки проблем.</span><span class="sxs-lookup"><span data-stu-id="6392a-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="6392a-168">Hello рекомендуется toofollow шаг #4.</span><span class="sxs-lookup"><span data-stu-id="6392a-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="6392a-169">Создайте конвейер с hello HDInsightHive действия.</span><span class="sxs-lookup"><span data-stu-id="6392a-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="6392a-170">Действие Hello процессов и преобразований данных hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-170">hello activity processes/transforms hello data.</span></span>

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="6392a-171">Развертывание конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="6392a-171">Deploy hello pipeline.</span></span> <span data-ttu-id="6392a-172">Дополнительные сведения см. в разделе [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6392a-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="6392a-173">Отслеживание с помощью мониторинга фабрики данных hello конвейера hello и административные представления.</span><span class="sxs-lookup"><span data-stu-id="6392a-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="6392a-174">Подробные сведения см. в статье [Мониторинг конвейеров фабрики данных и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6392a-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="6392a-175">Настройка параметров для сценария Hive</span><span class="sxs-lookup"><span data-stu-id="6392a-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="6392a-176">В этом примере журналы игры ежедневно добавляются в хранилище BLOB-объектов Azure и хранятся в папках, разбитых по дате и времени.</span><span class="sxs-lookup"><span data-stu-id="6392a-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="6392a-177">Требуется, чтобы скрипт Hive tooparameterize hello и передать входные папку hello динамически во время выполнения, а также выходом hello, разбитый на дату и время.</span><span class="sxs-lookup"><span data-stu-id="6392a-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="6392a-178">toouse параметризованные скрипт Hive, выполните следующие hello</span><span class="sxs-lookup"><span data-stu-id="6392a-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="6392a-179">Задать параметры hello в **определяет**.</span><span class="sxs-lookup"><span data-stu-id="6392a-179">Define hello parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* <span data-ttu-id="6392a-180">В hello скрипт Hive ссылаться с помощью параметра toohello **${hiveconf: ParameterName}**.</span><span class="sxs-lookup"><span data-stu-id="6392a-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="6392a-181">См. также</span><span class="sxs-lookup"><span data-stu-id="6392a-181">See Also</span></span>
* [<span data-ttu-id="6392a-182">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="6392a-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="6392a-183">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="6392a-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="6392a-184">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="6392a-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="6392a-185">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="6392a-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="6392a-186">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="6392a-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

