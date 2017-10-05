---
title: "Преобразование данных с помощью действия Hive в Azure | Документация Майкрософт"
description: "Узнайте, как с помощью действия Hive в фабрике данных Azure выполнять запросы Hive к кластеру HDInsight по требованию или собственному кластеру HDInsight."
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
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="ba6db-103">Преобразование данных с помощью действия Hive в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="ba6db-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ba6db-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="ba6db-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ba6db-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="ba6db-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ba6db-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="ba6db-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ba6db-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="ba6db-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ba6db-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="ba6db-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ba6db-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ba6db-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ba6db-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ba6db-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ba6db-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="ba6db-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ba6db-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ba6db-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ba6db-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="ba6db-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="ba6db-114">Действие Hive HDInsight в [конвейере](data-factory-create-pipelines.md) фабрики данных выполняет запросы Hive к [вашему собственному](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) кластеру HDInsight или кластеру HDInsight [по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="ba6db-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ba6db-115">Данная статья основана на материалах статьи о [действиях преобразования данных](data-factory-data-transformation-activities.md) , в которой приведен общий обзор преобразования данных и список поддерживаемых действий преобразования.</span><span class="sxs-lookup"><span data-stu-id="ba6db-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="ba6db-116">Если вы не знакомы с фабрикой данных Azure, сначала ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md) и руководством [Создание первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ba6db-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="ba6db-117">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ba6db-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="ba6db-118">Сведения о синтаксисе</span><span class="sxs-lookup"><span data-stu-id="ba6db-118">Syntax details</span></span>
| <span data-ttu-id="ba6db-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="ba6db-119">Property</span></span> | <span data-ttu-id="ba6db-120">Описание</span><span class="sxs-lookup"><span data-stu-id="ba6db-120">Description</span></span> | <span data-ttu-id="ba6db-121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ba6db-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba6db-122">name</span><span class="sxs-lookup"><span data-stu-id="ba6db-122">name</span></span> |<span data-ttu-id="ba6db-123">Имя действия.</span><span class="sxs-lookup"><span data-stu-id="ba6db-123">Name of the activity</span></span> |<span data-ttu-id="ba6db-124">Да</span><span class="sxs-lookup"><span data-stu-id="ba6db-124">Yes</span></span> |
| <span data-ttu-id="ba6db-125">Описание</span><span class="sxs-lookup"><span data-stu-id="ba6db-125">description</span></span> |<span data-ttu-id="ba6db-126">Текст, описывающий, для чего используется действие</span><span class="sxs-lookup"><span data-stu-id="ba6db-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="ba6db-127">Нет</span><span class="sxs-lookup"><span data-stu-id="ba6db-127">No</span></span> |
| <span data-ttu-id="ba6db-128">type</span><span class="sxs-lookup"><span data-stu-id="ba6db-128">type</span></span> |<span data-ttu-id="ba6db-129">HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="ba6db-129">HDinsightHive</span></span> |<span data-ttu-id="ba6db-130">Да</span><span class="sxs-lookup"><span data-stu-id="ba6db-130">Yes</span></span> |
| <span data-ttu-id="ba6db-131">inputs</span><span class="sxs-lookup"><span data-stu-id="ba6db-131">inputs</span></span> |<span data-ttu-id="ba6db-132">Входные данные, используемые действием Hive</span><span class="sxs-lookup"><span data-stu-id="ba6db-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="ba6db-133">Нет</span><span class="sxs-lookup"><span data-stu-id="ba6db-133">No</span></span> |
| <span data-ttu-id="ba6db-134">outputs</span><span class="sxs-lookup"><span data-stu-id="ba6db-134">outputs</span></span> |<span data-ttu-id="ba6db-135">Выходные данные, создаваемые действием Hive</span><span class="sxs-lookup"><span data-stu-id="ba6db-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="ba6db-136">Да</span><span class="sxs-lookup"><span data-stu-id="ba6db-136">Yes</span></span> |
| <span data-ttu-id="ba6db-137">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="ba6db-137">linkedServiceName</span></span> |<span data-ttu-id="ba6db-138">Ссылка на кластер HDInsight, зарегистрированный в качестве связанной службы в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="ba6db-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="ba6db-139">Да</span><span class="sxs-lookup"><span data-stu-id="ba6db-139">Yes</span></span> |
| <span data-ttu-id="ba6db-140">script</span><span class="sxs-lookup"><span data-stu-id="ba6db-140">script</span></span> |<span data-ttu-id="ba6db-141">Указывается встроенный сценарий Hive.</span><span class="sxs-lookup"><span data-stu-id="ba6db-141">Specify the Hive script inline</span></span> |<span data-ttu-id="ba6db-142">Нет</span><span class="sxs-lookup"><span data-stu-id="ba6db-142">No</span></span> |
| <span data-ttu-id="ba6db-143">script path</span><span class="sxs-lookup"><span data-stu-id="ba6db-143">script path</span></span> |<span data-ttu-id="ba6db-144">Путь к файлу сценария Hive в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ba6db-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="ba6db-145">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="ba6db-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="ba6db-146">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="ba6db-146">Both cannot be used together.</span></span> <span data-ttu-id="ba6db-147">В имени файла учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="ba6db-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="ba6db-148">Нет</span><span class="sxs-lookup"><span data-stu-id="ba6db-148">No</span></span> |
| <span data-ttu-id="ba6db-149">defines</span><span class="sxs-lookup"><span data-stu-id="ba6db-149">defines</span></span> |<span data-ttu-id="ba6db-150">Параметры в виде пары "ключ-значение", ссылки на которые указываются в сценарии Hive с помощью элемента hiveconf.</span><span class="sxs-lookup"><span data-stu-id="ba6db-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="ba6db-151">Нет</span><span class="sxs-lookup"><span data-stu-id="ba6db-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="ba6db-152">Пример</span><span class="sxs-lookup"><span data-stu-id="ba6db-152">Example</span></span>
<span data-ttu-id="ba6db-153">Рассмотрим пример с аналитикой игровых журналов. Предположим, вы хотите определить время, которое пользователи проводят за игрой, выпущенной вашей компанией.</span><span class="sxs-lookup"><span data-stu-id="ba6db-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="ba6db-154">Ниже приведен журнал игры с разделителями-запятыми (`,`), содержащий следующие поля: ProfileID, SessionStart, Duration, SrcIPAddress и GameType.</span><span class="sxs-lookup"><span data-stu-id="ba6db-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="ba6db-155">**Сценарий Hive** для обработки этих данных выглядит так:</span><span class="sxs-lookup"><span data-stu-id="ba6db-155">The **Hive script** to process this data:</span></span>

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

<span data-ttu-id="ba6db-156">Чтобы выполнить его в конвейере фабрики данных, необходимо сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="ba6db-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="ba6db-157">Создайте связанную службу для регистрации [собственного вычислительного кластера HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или настройте [вычислительный кластер HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ba6db-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="ba6db-158">Назовем эту связанную службу HDInsightLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ba6db-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="ba6db-159">Создайте [связанную службу](data-factory-azure-blob-connector.md) для настройки подключения к хранилищу BLOB-объектов Azure, в котором хранятся данные.</span><span class="sxs-lookup"><span data-stu-id="ba6db-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="ba6db-160">Назовем эту связанную службу StorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ba6db-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="ba6db-161">Создайте [наборы данных](data-factory-create-datasets.md) , указывающие на входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ba6db-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="ba6db-162">Назовем входной набор данных HiveSampleIn, а выходной — HiveSampleOut.</span><span class="sxs-lookup"><span data-stu-id="ba6db-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="ba6db-163">Скопируйте запрос Hive в файл и сохраните его в хранилище BLOB-объектов Azure, настроенном на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="ba6db-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="ba6db-164">Если хранилище, в котором размещаются данные, отличается от хранилища, в котором размещаются этот файл запроса, создайте отдельную связанную службу хранилища Azure и добавьте ссылку на нее в действие.</span><span class="sxs-lookup"><span data-stu-id="ba6db-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="ba6db-165">Используйте свойство **scriptPath **, чтобы указать путь к файлу запроса Hive, и **scriptLinkedService**, чтобы определить службу хранилища Azure, содержащую файл сценария.</span><span class="sxs-lookup"><span data-stu-id="ba6db-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ba6db-166">Также можно добавить сценарий Hive непосредственно в определение действия, используя свойство **script** .</span><span class="sxs-lookup"><span data-stu-id="ba6db-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="ba6db-167">Мы не рекомендуем это делать, так как вам потребуется экранировать все специальные знаки в сценарии в документе JSON, что может вызвать проблемы при отладке.</span><span class="sxs-lookup"><span data-stu-id="ba6db-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="ba6db-168">Мы рекомендуем следовать инструкциям, описанным в шаге 4.</span><span class="sxs-lookup"><span data-stu-id="ba6db-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="ba6db-169">Создайте конвейер с действием HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="ba6db-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="ba6db-170">Это действие обрабатывает и преобразует данные.</span><span class="sxs-lookup"><span data-stu-id="ba6db-170">The activity processes/transforms the data.</span></span>

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
6. <span data-ttu-id="ba6db-171">Разверните конвейер.</span><span class="sxs-lookup"><span data-stu-id="ba6db-171">Deploy the pipeline.</span></span> <span data-ttu-id="ba6db-172">Дополнительные сведения см. в разделе [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ba6db-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="ba6db-173">Отслеживайте состояние конвейера, используя функции мониторинга и управления фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ba6db-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="ba6db-174">Подробные сведения см. в статье [Мониторинг конвейеров фабрики данных и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ba6db-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="ba6db-175">Настройка параметров для сценария Hive</span><span class="sxs-lookup"><span data-stu-id="ba6db-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="ba6db-176">В этом примере журналы игры ежедневно добавляются в хранилище BLOB-объектов Azure и хранятся в папках, разбитых по дате и времени.</span><span class="sxs-lookup"><span data-stu-id="ba6db-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="ba6db-177">Вам необходимо параметризовать сценарий Hive, чтобы адрес входной папки передавался во время выполнения динамически, а выходной набор данных сегментировался по дате и времени.</span><span class="sxs-lookup"><span data-stu-id="ba6db-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="ba6db-178">Чтобы использовать параметризованный сценарий Hive, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ba6db-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="ba6db-179">Задайте параметры в разделе **defines**.</span><span class="sxs-lookup"><span data-stu-id="ba6db-179">Define the parameters in **defines**.</span></span>

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
* <span data-ttu-id="ba6db-180">Добавьте ссылку на параметр в сценарий Hive с помощью элемента **${hiveconf:parameterName}**.</span><span class="sxs-lookup"><span data-stu-id="ba6db-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="ba6db-181">См. также</span><span class="sxs-lookup"><span data-stu-id="ba6db-181">See Also</span></span>
* [<span data-ttu-id="ba6db-182">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="ba6db-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="ba6db-183">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="ba6db-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="ba6db-184">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="ba6db-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="ba6db-185">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="ba6db-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="ba6db-186">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="ba6db-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

