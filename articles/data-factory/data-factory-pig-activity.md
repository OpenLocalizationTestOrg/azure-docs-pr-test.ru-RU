---
title: "Преобразование данных с помощью действия Pig в фабрике данных Azure | Документация Майкрософт"
description: "Узнайте, как с помощью действия Pig в фабрике данных Azure выполнять запросы Pig к собственному кластеру HDInsight или к кластеру HDInsight по требованию."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="ca4fb-103">Преобразование данных с помощью действия Pig в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="ca4fb-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ca4fb-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="ca4fb-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ca4fb-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="ca4fb-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ca4fb-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="ca4fb-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ca4fb-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="ca4fb-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ca4fb-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="ca4fb-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ca4fb-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ca4fb-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ca4fb-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="ca4fb-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ca4fb-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="ca4fb-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ca4fb-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ca4fb-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ca4fb-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="ca4fb-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="ca4fb-114">Действие Pig HDInsight в [конвейере](data-factory-create-pipelines.md) фабрики данных выполняет запросы Pig к [вашему собственному](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) кластеру HDInsight или кластеру HDInsight [по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ca4fb-115">Данная статья основана на материалах статьи о [действиях преобразования данных](data-factory-data-transformation-activities.md) , в которой приведен общий обзор преобразования данных и список поддерживаемых действий преобразования.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="ca4fb-116">Если вы не знакомы с фабрикой данных Azure, сначала ознакомьтесь со статьей [Введение в фабрику данных Azure](data-factory-introduction.md) и руководством [Создание первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ca4fb-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="ca4fb-117">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ca4fb-117">Syntax</span></span>

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
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
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a><span data-ttu-id="ca4fb-118">Сведения о синтаксисе</span><span class="sxs-lookup"><span data-stu-id="ca4fb-118">Syntax details</span></span>
| <span data-ttu-id="ca4fb-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="ca4fb-119">Property</span></span> | <span data-ttu-id="ca4fb-120">Описание</span><span class="sxs-lookup"><span data-stu-id="ca4fb-120">Description</span></span> | <span data-ttu-id="ca4fb-121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="ca4fb-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca4fb-122">name</span><span class="sxs-lookup"><span data-stu-id="ca4fb-122">name</span></span> |<span data-ttu-id="ca4fb-123">Имя действия.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-123">Name of the activity</span></span> |<span data-ttu-id="ca4fb-124">Да</span><span class="sxs-lookup"><span data-stu-id="ca4fb-124">Yes</span></span> |
| <span data-ttu-id="ca4fb-125">Описание</span><span class="sxs-lookup"><span data-stu-id="ca4fb-125">description</span></span> |<span data-ttu-id="ca4fb-126">Текст, описывающий, для чего используется действие</span><span class="sxs-lookup"><span data-stu-id="ca4fb-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="ca4fb-127">Нет</span><span class="sxs-lookup"><span data-stu-id="ca4fb-127">No</span></span> |
| <span data-ttu-id="ca4fb-128">type</span><span class="sxs-lookup"><span data-stu-id="ca4fb-128">type</span></span> |<span data-ttu-id="ca4fb-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="ca4fb-129">HDinsightPig</span></span> |<span data-ttu-id="ca4fb-130">Да</span><span class="sxs-lookup"><span data-stu-id="ca4fb-130">Yes</span></span> |
| <span data-ttu-id="ca4fb-131">inputs</span><span class="sxs-lookup"><span data-stu-id="ca4fb-131">inputs</span></span> |<span data-ttu-id="ca4fb-132">Входные данные, используемые действием Pig.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="ca4fb-133">Нет</span><span class="sxs-lookup"><span data-stu-id="ca4fb-133">No</span></span> |
| <span data-ttu-id="ca4fb-134">outputs</span><span class="sxs-lookup"><span data-stu-id="ca4fb-134">outputs</span></span> |<span data-ttu-id="ca4fb-135">Выходные данные, создаваемые действием Pig.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="ca4fb-136">Да</span><span class="sxs-lookup"><span data-stu-id="ca4fb-136">Yes</span></span> |
| <span data-ttu-id="ca4fb-137">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="ca4fb-137">linkedServiceName</span></span> |<span data-ttu-id="ca4fb-138">Ссылка на кластер HDInsight, зарегистрированный в качестве связанной службы в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="ca4fb-139">Да</span><span class="sxs-lookup"><span data-stu-id="ca4fb-139">Yes</span></span> |
| <span data-ttu-id="ca4fb-140">script</span><span class="sxs-lookup"><span data-stu-id="ca4fb-140">script</span></span> |<span data-ttu-id="ca4fb-141">Указывается встроенный сценарий Pig.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-141">Specify the Pig script inline</span></span> |<span data-ttu-id="ca4fb-142">Нет</span><span class="sxs-lookup"><span data-stu-id="ca4fb-142">No</span></span> |
| <span data-ttu-id="ca4fb-143">script path</span><span class="sxs-lookup"><span data-stu-id="ca4fb-143">script path</span></span> |<span data-ttu-id="ca4fb-144">Путь к файлу сценария Pig в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="ca4fb-145">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="ca4fb-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="ca4fb-146">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-146">Both cannot be used together.</span></span> <span data-ttu-id="ca4fb-147">В имени файла учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="ca4fb-148">Нет</span><span class="sxs-lookup"><span data-stu-id="ca4fb-148">No</span></span> |
| <span data-ttu-id="ca4fb-149">defines</span><span class="sxs-lookup"><span data-stu-id="ca4fb-149">defines</span></span> |<span data-ttu-id="ca4fb-150">Параметры в виде пары "ключ — значение", ссылки на которые указываются в сценарии Pig.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="ca4fb-151">Нет</span><span class="sxs-lookup"><span data-stu-id="ca4fb-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="ca4fb-152">Пример</span><span class="sxs-lookup"><span data-stu-id="ca4fb-152">Example</span></span>
<span data-ttu-id="ca4fb-153">Рассмотрим пример с аналитикой игровых журналов. Предположим, вы хотите определить время, которое игроки проводят за игрой, выпущенной вашей компанией.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="ca4fb-154">Ниже приведен журнал игры в формате CSV-файла.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="ca4fb-155">Он содержит следующие поля: ProfileID, SessionStart, Duration, SrcIPAddress и GameType.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="ca4fb-156">**Сценарий Pig** для обработки этих данных выглядит так:</span><span class="sxs-lookup"><span data-stu-id="ca4fb-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="ca4fb-157">Чтобы выполнить его в конвейере фабрики данных, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ca4fb-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="ca4fb-158">Создайте связанную службу для регистрации [собственного вычислительного кластера HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или настройте [вычислительный кластер HDInsight по запросу](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="ca4fb-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="ca4fb-159">Назовем эту связанную службу **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="ca4fb-160">Создайте [связанную службу](data-factory-azure-blob-connector.md) для настройки подключения к хранилищу BLOB-объектов Azure, в котором хранятся данные.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="ca4fb-161">Назовем эту связанную службу **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="ca4fb-162">Создайте [наборы данных](data-factory-create-datasets.md) , указывающие на входные и выходные данные.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="ca4fb-163">Назовем входной набор данных **PigSampleIn**, а выходной — **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="ca4fb-164">Скопируйте запрос Pig в файл, настроенный хранилищем BLOB-объектов Azure на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="ca4fb-165">Если хранилище BLOB-объектов Azure, размещающее данные, отличается от хранилища, размещающего файл запроса, то создайте отдельную связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="ca4fb-166">Добавьте ссылку на эту связанную службу в конфигурации действия.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="ca4fb-167">Используйте свойство scriptPath для указания пути к файлу сценария Pig и **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="ca4fb-168">Также можно добавить сценарий Pig непосредственно в определение действия, используя свойство **script** .</span><span class="sxs-lookup"><span data-stu-id="ca4fb-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="ca4fb-169">Однако мы не рекомендуем это делать, так как в этом случае потребуется экранировать все специальные знаки в сценарии, что может вызвать проблемы при отладке.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="ca4fb-170">Мы рекомендуем следовать инструкциям, описанным в шаге 4.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="ca4fb-171">Создайте конвейер с действием HDInsightPig.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="ca4fb-172">Это действие обрабатывает входные данные, запуская сценарий Pig в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. <span data-ttu-id="ca4fb-173">Разверните конвейер.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-173">Deploy the pipeline.</span></span> <span data-ttu-id="ca4fb-174">Дополнительные сведения см. в разделе [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ca4fb-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="ca4fb-175">Отслеживайте состояние конвейера, используя функции мониторинга и управления фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="ca4fb-176">Подробные сведения см. в статье [Мониторинг конвейеров фабрики данных и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ca4fb-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="ca4fb-177">Указание параметров для сценария Pig</span><span class="sxs-lookup"><span data-stu-id="ca4fb-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="ca4fb-178">Рассмотрим следующий пример: журналы игры ежедневно добавляются в хранилище BLOB-объектов Azure и хранятся в папках, разбитых по дате и времени.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="ca4fb-179">Вам необходимо параметризовать сценарий Pig так, чтобы адрес входной папки передавался во время выполнения динамически, а выходной набор данных также сегментировался по дате и времени.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="ca4fb-180">Чтобы использовать параметризованный сценарии Pig, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="ca4fb-181">Задайте параметры в разделе **defines**.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-181">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* <span data-ttu-id="ca4fb-182">В сценарии Pig сошлитесь на параметры с помощью**$parameterName**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ca4fb-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="ca4fb-183">См. также</span><span class="sxs-lookup"><span data-stu-id="ca4fb-183">See Also</span></span>
* [<span data-ttu-id="ca4fb-184">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="ca4fb-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="ca4fb-185">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="ca4fb-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="ca4fb-186">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="ca4fb-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="ca4fb-187">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="ca4fb-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="ca4fb-188">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="ca4fb-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

