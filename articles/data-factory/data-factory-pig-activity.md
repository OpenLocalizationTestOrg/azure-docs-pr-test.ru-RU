---
title: "Использование Pig действия в фабрике данных Azure данных aaaTransform | Документы Microsoft"
description: "Дополнительные сведения об использовании hello действие Pig в скриптах Pig toorun фабрики данных Azure в кластере HDInsight на запросу или свой собственный."
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
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="1d4c9-103">Преобразование данных с помощью действия Pig в фабрике данных Azure</span><span class="sxs-lookup"><span data-stu-id="1d4c9-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1d4c9-104">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="1d4c9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1d4c9-105">Действие Pig</span><span class="sxs-lookup"><span data-stu-id="1d4c9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1d4c9-106">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="1d4c9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1d4c9-107">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="1d4c9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1d4c9-108">Действие Spark</span><span class="sxs-lookup"><span data-stu-id="1d4c9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1d4c9-109">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="1d4c9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1d4c9-110">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="1d4c9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1d4c9-111">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="1d4c9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1d4c9-112">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1d4c9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1d4c9-113">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="1d4c9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="1d4c9-114">Hello действие Pig с HDInsight в фабрике данных [конвейера](data-factory-create-pipelines.md) выполняет запросы Pig на [собственные](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или [по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) кластера HDInsight под управлением Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1d4c9-115">Эта статья основана на hello [действия преобразования данных](data-factory-data-transformation-activities.md) статьи, которая дан обзор преобразования данных и hello поддерживается преобразование действий.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="1d4c9-116">Если новый tooAzure фабрики данных, прочтите [tooAzure введение фабрики данных](data-factory-introduction.md) и hello учебника: [создания вашего первого конвейера данных](data-factory-build-your-first-pipeline.md) перед считыванием в этой статье.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="1d4c9-117">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="1d4c9-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="1d4c9-118">Сведения о синтаксисе</span><span class="sxs-lookup"><span data-stu-id="1d4c9-118">Syntax details</span></span>
| <span data-ttu-id="1d4c9-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="1d4c9-119">Property</span></span> | <span data-ttu-id="1d4c9-120">Описание</span><span class="sxs-lookup"><span data-stu-id="1d4c9-120">Description</span></span> | <span data-ttu-id="1d4c9-121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1d4c9-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1d4c9-122">name</span><span class="sxs-lookup"><span data-stu-id="1d4c9-122">name</span></span> |<span data-ttu-id="1d4c9-123">Имя действия hello</span><span class="sxs-lookup"><span data-stu-id="1d4c9-123">Name of hello activity</span></span> |<span data-ttu-id="1d4c9-124">Да</span><span class="sxs-lookup"><span data-stu-id="1d4c9-124">Yes</span></span> |
| <span data-ttu-id="1d4c9-125">Описание</span><span class="sxs-lookup"><span data-stu-id="1d4c9-125">description</span></span> |<span data-ttu-id="1d4c9-126">Текст, описывающий, какое действие hello используется для</span><span class="sxs-lookup"><span data-stu-id="1d4c9-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="1d4c9-127">Нет</span><span class="sxs-lookup"><span data-stu-id="1d4c9-127">No</span></span> |
| <span data-ttu-id="1d4c9-128">type</span><span class="sxs-lookup"><span data-stu-id="1d4c9-128">type</span></span> |<span data-ttu-id="1d4c9-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="1d4c9-129">HDinsightPig</span></span> |<span data-ttu-id="1d4c9-130">Да</span><span class="sxs-lookup"><span data-stu-id="1d4c9-130">Yes</span></span> |
| <span data-ttu-id="1d4c9-131">inputs</span><span class="sxs-lookup"><span data-stu-id="1d4c9-131">inputs</span></span> |<span data-ttu-id="1d4c9-132">Один или несколько входов занятая hello действие Pig</span><span class="sxs-lookup"><span data-stu-id="1d4c9-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="1d4c9-133">Нет</span><span class="sxs-lookup"><span data-stu-id="1d4c9-133">No</span></span> |
| <span data-ttu-id="1d4c9-134">outputs</span><span class="sxs-lookup"><span data-stu-id="1d4c9-134">outputs</span></span> |<span data-ttu-id="1d4c9-135">Один или несколько выходов созданные hello действие Pig</span><span class="sxs-lookup"><span data-stu-id="1d4c9-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="1d4c9-136">Да</span><span class="sxs-lookup"><span data-stu-id="1d4c9-136">Yes</span></span> |
| <span data-ttu-id="1d4c9-137">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="1d4c9-137">linkedServiceName</span></span> |<span data-ttu-id="1d4c9-138">Кластер HDInsight toohello ссылка зарегистрирован как связанной службы в фабрике данных</span><span class="sxs-lookup"><span data-stu-id="1d4c9-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="1d4c9-139">Да</span><span class="sxs-lookup"><span data-stu-id="1d4c9-139">Yes</span></span> |
| <span data-ttu-id="1d4c9-140">script</span><span class="sxs-lookup"><span data-stu-id="1d4c9-140">script</span></span> |<span data-ttu-id="1d4c9-141">Укажите встроенного скрипта Pig hello</span><span class="sxs-lookup"><span data-stu-id="1d4c9-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="1d4c9-142">Нет</span><span class="sxs-lookup"><span data-stu-id="1d4c9-142">No</span></span> |
| <span data-ttu-id="1d4c9-143">script path</span><span class="sxs-lookup"><span data-stu-id="1d4c9-143">script path</span></span> |<span data-ttu-id="1d4c9-144">Хранить сценарий Pig hello в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="1d4c9-145">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="1d4c9-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="1d4c9-146">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-146">Both cannot be used together.</span></span> <span data-ttu-id="1d4c9-147">Имя файла Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="1d4c9-148">Нет</span><span class="sxs-lookup"><span data-stu-id="1d4c9-148">No</span></span> |
| <span data-ttu-id="1d4c9-149">defines</span><span class="sxs-lookup"><span data-stu-id="1d4c9-149">defines</span></span> |<span data-ttu-id="1d4c9-150">Укажите параметры как пары "ключ значение" для ссылки в пределах hello сценарий Pig</span><span class="sxs-lookup"><span data-stu-id="1d4c9-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="1d4c9-151">Нет</span><span class="sxs-lookup"><span data-stu-id="1d4c9-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="1d4c9-152">Пример</span><span class="sxs-lookup"><span data-stu-id="1d4c9-152">Example</span></span>
<span data-ttu-id="1d4c9-153">Давайте рассмотрим пример игры журналы аналитики, место tooidentify hello времени, затраченного игроки, игры, запускаемого по вашей компании.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="1d4c9-154">Следующий пример игры журнала Hello — это файл запятыми (,).</span><span class="sxs-lookup"><span data-stu-id="1d4c9-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="1d4c9-155">Он содержит следующие поля — ProfileID, SessionStart, длительность, SrcIPAddress и GameType hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="1d4c9-156">Hello **сценарий Pig** tooprocess эти данные:</span><span class="sxs-lookup"><span data-stu-id="1d4c9-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="1d4c9-157">tooexecute Pig для этого сценария в конвейере фабрики данных hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="1d4c9-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="1d4c9-158">Создание tooregister связанной службы [собственные HDInsight вычислительный кластер](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) или настроить [вычислительный кластер HDInsight по требованию](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1d4c9-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="1d4c9-159">Назовем эту связанную службу **HDInsightLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="1d4c9-160">Создание [связанная служба](data-factory-azure-blob-connector.md) tooconfigure hello подключения tooAzure хранилища BLOB-данных размещение данных hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="1d4c9-161">Назовем эту связанную службу **StorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="1d4c9-162">Создание [наборы данных](data-factory-create-datasets.md) и toohello входных данных, а затем hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="1d4c9-163">Давайте назовем входного набора данных hello **PigSampleIn** и hello выходной набор данных **PigSampleOut**.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="1d4c9-164">Скопируйте запрос Pig hello в файл hello хранилища больших двоичных объектов, настроенную на шаге #2.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="1d4c9-165">Если hello хранилища Azure, на котором размещена hello данных отличается от hello один, на котором размещается файл запрос hello, создайте отдельный связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="1d4c9-166">См. в связанных toohello службы в конфигурации действия hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="1d4c9-167">Используйте ** scriptPath ** файл сценария toopig путь hello toospecify и **scriptLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1d4c9-168">Можно также предоставить с помощью hello hello встроенного скрипта Pig в определении действия hello **сценарий** свойство.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="1d4c9-169">Однако не рекомендуется этот подход, как все специальные символы в скрипте hello должен toobe escape-последовательность и может вызвать проблемы отладки.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="1d4c9-170">Hello рекомендуется toofollow шаг #4.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="1d4c9-171">Создайте конвейер hello с hello HDInsightPig действия.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="1d4c9-172">Это действие обрабатывает входные данные hello путем выполнения сценария Pig в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="1d4c9-173">Развертывание конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-173">Deploy hello pipeline.</span></span> <span data-ttu-id="1d4c9-174">Дополнительные сведения см. в разделе [Создание конвейеров](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1d4c9-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="1d4c9-175">Отслеживание с помощью мониторинга фабрики данных hello конвейера hello и административные представления.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="1d4c9-176">Подробные сведения см. в статье [Мониторинг конвейеров фабрики данных и управление ими](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1d4c9-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="1d4c9-177">Указание параметров для сценария Pig</span><span class="sxs-lookup"><span data-stu-id="1d4c9-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="1d4c9-178">Рассмотрим следующий пример hello: игры журналы, полученный ежедневно в хранилище больших двоичных объектов Azure и сохраняются в папке секционированные по дате и времени.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="1d4c9-179">Сценарий Pig tooparameterize hello и передать входные папку hello динамически во время выполнения, а также выходом hello, разбитый на дату и время.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="1d4c9-180">toouse параметризованные сценарий Pig, выполните hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="1d4c9-181">Задать параметры hello в **определяет**.</span><span class="sxs-lookup"><span data-stu-id="1d4c9-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="1d4c9-182">В hello сценарий Pig, ссылаетесь toohello параметров с помощью "**$parameterName**" как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="1d4c9-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="1d4c9-183">См. также</span><span class="sxs-lookup"><span data-stu-id="1d4c9-183">See Also</span></span>
* [<span data-ttu-id="1d4c9-184">Действие Hive</span><span class="sxs-lookup"><span data-stu-id="1d4c9-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="1d4c9-185">Действие MapReduce</span><span class="sxs-lookup"><span data-stu-id="1d4c9-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="1d4c9-186">Потоковая активность Hadoop</span><span class="sxs-lookup"><span data-stu-id="1d4c9-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="1d4c9-187">Вызов программ Spark</span><span class="sxs-lookup"><span data-stu-id="1d4c9-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="1d4c9-188">Вызов сценариев R</span><span class="sxs-lookup"><span data-stu-id="1d4c9-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

