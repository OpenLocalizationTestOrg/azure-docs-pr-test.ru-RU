---
title: "Планирование и исполнение с использованием фабрики данных | Документация Майкрософт"
description: "Сведения об аспектах планирования и исполнения в модели приложений фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="1ed3b-103">Планирование и исполнение с использованием фабрики данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="1ed3b-104">Здесь объясняются аспекты планирования и исполнения в модели приложений фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="1ed3b-105">В этой статье предполагается, что вам известны основные понятия модели приложений фабрики данных: действия, конвейеры, связанные службы и наборы данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="1ed3b-106">С основными понятиями фабрики данных Azure можно ознакомиться в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="1ed3b-107">Введение в службу фабрики данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="1ed3b-108">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="1ed3b-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="1ed3b-109">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="1ed3b-110">Время начала и окончания конвейера</span><span class="sxs-lookup"><span data-stu-id="1ed3b-110">Start and end times of pipeline</span></span>
<span data-ttu-id="1ed3b-111">Конвейер работает только в период активности, то есть между временем **начала** и **окончания**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="1ed3b-112">Он не работает до времени начала и после времени окончания.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="1ed3b-113">Если конвейер приостановлен, он не будет работать независимо от значений времени начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="1ed3b-114">Запустить конвейер можно только в том случае, если он не находится в приостановленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="1ed3b-115">Эти параметры (начало, окончание, остановка) можно найти в определении конвейера:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="1ed3b-116">Дополнительные сведения об этих свойствах см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="1ed3b-117">Указание расписания для действия</span><span class="sxs-lookup"><span data-stu-id="1ed3b-117">Specify schedule for an activity</span></span>
<span data-ttu-id="1ed3b-118">Выполняется не сам конвейер,</span><span class="sxs-lookup"><span data-stu-id="1ed3b-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="1ed3b-119">а действия в нем. Однако это происходит в общем контексте конвейера.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="1ed3b-120">С помощью раздела **scheduler** в файле действия JSON можно указать регулярное расписание данного действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="1ed3b-121">Например, можно запланировать выполнение действия каждый час следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="1ed3b-122">Как показано на схеме, при задании расписания для действия создается последовательность "переворачивающихся" окон в пределах времени начала и окончания конвейера.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="1ed3b-123">"Переворачивающиеся" окна — это ряд не перекрывающихся и не соприкасающихся интервалов фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="1ed3b-124">Эти логические стыкующиеся окна для действия называются **окнами действия**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Пример планировщика действий](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="1ed3b-126">Свойство **scheduler** для действия является необязательным.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="1ed3b-127">Если это свойство указывается, оно должно соответствовать периодичности, заданной в определении выходного набора данных для действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="1ed3b-128">Сейчас на основе этого набора настраивается расписание.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="1ed3b-129">Поэтому вы должны создать выходной набор данных, даже если действие не выдает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="1ed3b-130">Указание расписания для набора данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="1ed3b-131">У каждого действия в конвейере фабрики данных может быть несколько входных **наборов данных** или же ни одного, и каждое действие может производить один или несколько выходных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="1ed3b-132">Для действия можно указать периодичность, с которой поступают входные данные или выводятся выходные данные, используя раздел **availability** в определении набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="1ed3b-133">**frequency** в разделе **availability** указывает единицу времени.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="1ed3b-134">Допустимы следующие значения частоты: Minute, Hour, Day, Week и Month.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="1ed3b-135">Свойство **interval** в разделе availability задает множитель для частоты.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="1ed3b-136">Например, если для параметра frequency задано значение Day, а для interval — 1 для выходного набора данных, выходные данные будут создаваться ежедневно.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="1ed3b-137">Если вы выбрали значение Minute для параметра frequency, мы рекомендуем задать для параметра interval значение не менее 15.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="1ed3b-138">В следующем примере входные и выходные данные поступают каждый час (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="1ed3b-139">**Входной набор данных:**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="1ed3b-140">**Выходной набор данных**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="1ed3b-141">Сейчас **на основе этого набора настраивается расписание.**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="1ed3b-142">Другими словами, расписание, указанное для выходного набора данных, используется для запуска действия во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="1ed3b-143">Поэтому вы должны создать выходной набор данных, даже если действие не выдает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="1ed3b-144">Если действие не принимает никаких входных данных, входной набор данных можно не создавать.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="1ed3b-145">В следующем определении конвейера свойство **scheduler** используется, чтобы задать расписание для действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="1ed3b-146">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-146">This property is optional.</span></span> <span data-ttu-id="1ed3b-147">Сейчас расписание для действия должно соответствовать расписанию, указанному для выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="1ed3b-148">В этом примере действие выполняется каждый час между временем начала и окончания конвейера.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="1ed3b-149">Выходные данные создаются ежечасно в рамках трех часовых окон (с 8:00 до 9:00, с 9:00 до 10:00 и с 10:00 до 11:00).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="1ed3b-150">Каждая единица данных, потребляемых или создаваемых запуском действия, называется **срезом данных**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="1ed3b-151">На следующей схеме показан пример действия с входным и выходным наборами данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Планировщик доступности](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="1ed3b-153">На схеме показаны почасовые срезы данных для входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="1ed3b-154">На схеме показаны три входных среза, готовых к обработке.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="1ed3b-155">Выполняемое действие 11–10 AM выдает выходной срез 10–11 AM.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="1ed3b-156">К интервалу времени, связанному с текущим срезом, можно получить доступ в наборе данных JSON с помощью переменных [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) и [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="1ed3b-157">Аналогичным образом можно получить доступ к интервалу времени, связанному с окном действий, с помощью переменных WindowStart и WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="1ed3b-158">Расписание действия должно соответствовать расписанию выходного набора данных для действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="1ed3b-159">Таким образом значения SliceStart, SliceEnd, WindowStart и WindowEnd совпадают соответственно.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="1ed3b-160">Дополнительные сведения об этих переменных см. в статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="1ed3b-161">Эти переменные можно использовать для различных целей в действии JSON.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="1ed3b-162">Например, для выбора данных из входных и выходных наборов данных, соответствующих временным рядам (к примеру, с 8:00 до 9:00).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="1ed3b-163">В примере значения **WindowStart** и **WindowEnd** используются, чтобы выбрать соответствующие данные для выполнения действия и скопировать их в большой двоичный объект с соответствующим значением **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="1ed3b-164">Значение **folderPath** параметризовано таким образом, чтобы каждый час использовалась отдельная папка.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="1ed3b-165">В предыдущем примере используется то же расписание (ежечасно), указанное для входных и выходных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="1ed3b-166">Если входной набор данных для действия выводится с другой частотой, скажем, каждые 15 минут, действие, создающее этот выходной набор данных, по-прежнему выполняется раз в час, так как на основе этого набора настраивается расписание действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="1ed3b-167">Дополнительные сведения см. в разделе [Моделирование наборов данных с разной частотой](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="1ed3b-168">Доступность набора данных и политики</span><span class="sxs-lookup"><span data-stu-id="1ed3b-168">Dataset availability and policies</span></span>
<span data-ttu-id="1ed3b-169">Вы узнали об использовании свойств frequency и interval в разделе availability определения набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="1ed3b-170">Есть и другие свойства, влияющие на планирование и выполнение действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="1ed3b-171">Доступность набора данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-171">Dataset availability</span></span> 
<span data-ttu-id="1ed3b-172">В таблице ниже перечислены свойства, которые можно использовать в разделе **availability**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="1ed3b-173">Свойство</span><span class="sxs-lookup"><span data-stu-id="1ed3b-173">Property</span></span> | <span data-ttu-id="1ed3b-174">Описание</span><span class="sxs-lookup"><span data-stu-id="1ed3b-174">Description</span></span> | <span data-ttu-id="1ed3b-175">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1ed3b-175">Required</span></span> | <span data-ttu-id="1ed3b-176">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1ed3b-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ed3b-177">frequency</span><span class="sxs-lookup"><span data-stu-id="1ed3b-177">frequency</span></span> |<span data-ttu-id="1ed3b-178">Указывает единицу времени, которая определяет частоту создания среза данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="1ed3b-179"><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="1ed3b-180">Да</span><span class="sxs-lookup"><span data-stu-id="1ed3b-180">Yes</span></span> |<span data-ttu-id="1ed3b-181">Нет данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-181">NA</span></span> |
| <span data-ttu-id="1ed3b-182">interval</span><span class="sxs-lookup"><span data-stu-id="1ed3b-182">interval</span></span> |<span data-ttu-id="1ed3b-183">Задает множитель для частоты.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="1ed3b-184">"Интервал х частоты" определяет частоту создания срезов.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="1ed3b-185">Если нужно, чтобы срез в наборе данных создавался каждый час, задайте для параметра <b>frequency</b> значение <b>Hour</b>, а для параметра <b>interval</b> — значение <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="1ed3b-186"><b>Примечание.</b> Если вы выбрали значение Minute для параметра Frequency, рекомендуем, чтобы интервал длился не менее 15 минут.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="1ed3b-187">Да</span><span class="sxs-lookup"><span data-stu-id="1ed3b-187">Yes</span></span> |<span data-ttu-id="1ed3b-188">Нет данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-188">NA</span></span> |
| <span data-ttu-id="1ed3b-189">style</span><span class="sxs-lookup"><span data-stu-id="1ed3b-189">style</span></span> |<span data-ttu-id="1ed3b-190">Указывает, когда выполняется срез: в начале или в конце интервала.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="1ed3b-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="1ed3b-191">StartOfInterval</span></span></li><li><span data-ttu-id="1ed3b-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="1ed3b-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="1ed3b-193">Если для Frequency задано значение Month, а для Style — EndOfInterval, срез данных будет создаваться в последний день месяца.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="1ed3b-194">Если для Style задано значение StartOfInterval, срез создается в первый день месяца.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="1ed3b-195">Если для frequency задано значение Day, а для style — EndOfInterval, срез данных будет создаваться в последний час дня.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="1ed3b-196">Если для Frequency задано значение Hour, а для Style — EndOfInterval, срез создается в конце часа.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="1ed3b-197">Например, для периода с 13:00 до 14:00 срез создается в 14:00.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="1ed3b-198">Нет</span><span class="sxs-lookup"><span data-stu-id="1ed3b-198">No</span></span> |<span data-ttu-id="1ed3b-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="1ed3b-199">EndOfInterval</span></span> |
| <span data-ttu-id="1ed3b-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="1ed3b-200">anchorDateTime</span></span> |<span data-ttu-id="1ed3b-201">Определяет момент времени, на основе которого планировщик вычисляет границы среза набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="1ed3b-202"><b>Примечание</b>. Если параметр AnchorDateTime содержит элементы с большей степенью детализации, чем значение параметра frequency, эти элементы игнорируются.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="1ed3b-203">Например, если для <b>интервала</b> задано значение <b>ежечасно</b> (frequency = Hour, interval = 1), а <b>AnchorDateTime</b> содержит <b>минуты и секунды</b>, то <b>минуты и секунды</b> из параметра AnchorDateTime не учитываются.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="1ed3b-204">Нет</span><span class="sxs-lookup"><span data-stu-id="1ed3b-204">No</span></span> |<span data-ttu-id="1ed3b-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="1ed3b-205">01/01/0001</span></span> |
| <span data-ttu-id="1ed3b-206">offset</span><span class="sxs-lookup"><span data-stu-id="1ed3b-206">offset</span></span> |<span data-ttu-id="1ed3b-207">Интервал времени, на который сдвигаются начало и конец всех срезов данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="1ed3b-208"><b>Примечание</b>. Если указаны значения для обоих параметров (anchorDateTime и offset), сдвиг вычисляется с учетом обоих значений.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="1ed3b-209">Нет</span><span class="sxs-lookup"><span data-stu-id="1ed3b-209">No</span></span> |<span data-ttu-id="1ed3b-210">Нет данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="1ed3b-211">Пример смещения</span><span class="sxs-lookup"><span data-stu-id="1ed3b-211">offset example</span></span>
<span data-ttu-id="1ed3b-212">По умолчанию создание ежедневных срезов (`"frequency": "Day", "interval": 1`) начинается в 00:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="1ed3b-213">Если требуется начинать их создание 06:00 (UTC), задайте смещение, как показано в следующем фрагменте.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="1ed3b-214">Пример для anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="1ed3b-214">anchorDateTime example</span></span>
<span data-ttu-id="1ed3b-215">В следующем примере набор данных создается каждые 23 часа.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="1ed3b-216">Создание первого среза начинается в момент, определяемый параметром anchorDateTime, для которого задано значение `2017-04-19T08:00:00` (время в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="1ed3b-217">Пример для Offset и Style</span><span class="sxs-lookup"><span data-stu-id="1ed3b-217">offset/style Example</span></span>
<span data-ttu-id="1ed3b-218">Следующий набор данных создается ежемесячно в 3-й день каждого месяца в 08:00 (`3.08:00:00`).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="1ed3b-219">Политика набора данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-219">Dataset policy</span></span>
<span data-ttu-id="1ed3b-220">Для набора данных можно определить политику проверки, указывающую, как данные, созданные выполнением среза, могут быть проверены на готовность к потреблению.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="1ed3b-221">В таких случаях после завершения выполнения среза состояние выходного среза меняется на **Ожидание** с подсостоянием **Проверка**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="1ed3b-222">После проверки срезов их статус меняется на **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="1ed3b-223">Если срез данных был сформирован, но не прошел проверку, запуски действий для нижестоящих срезов, зависимых от данного среза, не будут обрабатываться.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="1ed3b-224">[Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="1ed3b-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="1ed3b-225">Раздел **policy** в определении набора данных содержит условия, которым должен соответствовать срез данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="1ed3b-226">В таблице ниже перечислены свойства, которые можно использовать в разделе **policy**:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="1ed3b-227">Имя политики</span><span class="sxs-lookup"><span data-stu-id="1ed3b-227">Policy Name</span></span> | <span data-ttu-id="1ed3b-228">Описание</span><span class="sxs-lookup"><span data-stu-id="1ed3b-228">Description</span></span> | <span data-ttu-id="1ed3b-229">Применяется к</span><span class="sxs-lookup"><span data-stu-id="1ed3b-229">Applied To</span></span> | <span data-ttu-id="1ed3b-230">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1ed3b-230">Required</span></span> | <span data-ttu-id="1ed3b-231">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1ed3b-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="1ed3b-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="1ed3b-232">minimumSizeMB</span></span> | <span data-ttu-id="1ed3b-233">Проверяет, удовлетворяют ли данные в **большом двоичном объекте Azure** требованиям к минимальному размеру (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="1ed3b-234">большом двоичном объекте Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3b-234">Azure Blob</span></span> |<span data-ttu-id="1ed3b-235">Нет</span><span class="sxs-lookup"><span data-stu-id="1ed3b-235">No</span></span> |<span data-ttu-id="1ed3b-236">Нет данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-236">NA</span></span> |
| <span data-ttu-id="1ed3b-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="1ed3b-237">minimumRows</span></span> | <span data-ttu-id="1ed3b-238">Проверяет, содержат ли данные в **базе данных SQL Azure** или **таблице Azure** минимально необходимое количество строк.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="1ed3b-239">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3b-239">Azure SQL Database</span></span></li><li><span data-ttu-id="1ed3b-240">таблице Azure</span><span class="sxs-lookup"><span data-stu-id="1ed3b-240">Azure Table</span></span></li></ul> |<span data-ttu-id="1ed3b-241">Нет</span><span class="sxs-lookup"><span data-stu-id="1ed3b-241">No</span></span> |<span data-ttu-id="1ed3b-242">Нет данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="1ed3b-243">Примеры</span><span class="sxs-lookup"><span data-stu-id="1ed3b-243">Examples</span></span>
<span data-ttu-id="1ed3b-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="1ed3b-245">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="1ed3b-246">Дополнительные сведения о наборах данных см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="1ed3b-247">Политики действий</span><span class="sxs-lookup"><span data-stu-id="1ed3b-247">Activity policies</span></span>
<span data-ttu-id="1ed3b-248">Политики влияют на поведение во время выполнения действия, особенно при обработке среза таблицы.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="1ed3b-249">В следующей таблице приведено несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-249">The following table provides the details.</span></span>

| <span data-ttu-id="1ed3b-250">Свойство</span><span class="sxs-lookup"><span data-stu-id="1ed3b-250">Property</span></span> | <span data-ttu-id="1ed3b-251">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="1ed3b-251">Permitted values</span></span> | <span data-ttu-id="1ed3b-252">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1ed3b-252">Default Value</span></span> | <span data-ttu-id="1ed3b-253">Описание</span><span class="sxs-lookup"><span data-stu-id="1ed3b-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1ed3b-254">concurrency</span><span class="sxs-lookup"><span data-stu-id="1ed3b-254">concurrency</span></span> |<span data-ttu-id="1ed3b-255">Целое число </span><span class="sxs-lookup"><span data-stu-id="1ed3b-255">Integer</span></span> <br/><br/><span data-ttu-id="1ed3b-256">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="1ed3b-256">Max value: 10</span></span> |<span data-ttu-id="1ed3b-257">1</span><span class="sxs-lookup"><span data-stu-id="1ed3b-257">1</span></span> |<span data-ttu-id="1ed3b-258">Число одновременных выполнений действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="1ed3b-259">Определяет количество параллельных выполнений одного действия для обработки разных срезов.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="1ed3b-260">Например, высокое значение этого свойства ускорит обработку большого набора доступных данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="1ed3b-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="1ed3b-261">executionPriorityOrder</span></span> |<span data-ttu-id="1ed3b-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="1ed3b-262">NewestFirst</span></span><br/><br/><span data-ttu-id="1ed3b-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="1ed3b-263">OldestFirst</span></span> |<span data-ttu-id="1ed3b-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="1ed3b-264">OldestFirst</span></span> |<span data-ttu-id="1ed3b-265">Определяет порядок обработки срезов данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="1ed3b-266">Предположим, есть два ожидающих обработки среза (от 16:00 и от 17:00).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="1ed3b-267">Если для свойства executionPriorityOrder задано значение NewestFirst, срез от 17:00 будет обработан первым.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="1ed3b-268">Точно так же, если для executionPriorityORder задано значение OldestFIrst, первым будет обработан срез от 16:00.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="1ed3b-269">retry</span><span class="sxs-lookup"><span data-stu-id="1ed3b-269">retry</span></span> |<span data-ttu-id="1ed3b-270">Целое число </span><span class="sxs-lookup"><span data-stu-id="1ed3b-270">Integer</span></span><br/><br/><span data-ttu-id="1ed3b-271">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="1ed3b-271">Max value can be 10</span></span> |<span data-ttu-id="1ed3b-272">0</span><span class="sxs-lookup"><span data-stu-id="1ed3b-272">0</span></span> |<span data-ttu-id="1ed3b-273">Число повторных попыток обработки данных до того, как срез перейдет в состояние Failure (сбой).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="1ed3b-274">Выполнение действия со срезом данных повторяется указанное количество раз.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="1ed3b-275">Повторная попытка выполняется сразу после неудачной.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="1ed3b-276">timeout</span><span class="sxs-lookup"><span data-stu-id="1ed3b-276">timeout</span></span> |<span data-ttu-id="1ed3b-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1ed3b-277">TimeSpan</span></span> |<span data-ttu-id="1ed3b-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1ed3b-278">00:00:00</span></span> |<span data-ttu-id="1ed3b-279">Время ожидания для действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-279">Timeout for the activity.</span></span> <span data-ttu-id="1ed3b-280">Пример: 00:10:00 (время ожидания — 10 минут).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="1ed3b-281">Если значение не указано или равно 0, то время ожидания не ограничено.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="1ed3b-282">Если время обработки среза превышает время ожидания, система отменяет текущую обработку и начинает новую.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="1ed3b-283">Количество повторов зависит от значения свойства retry.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="1ed3b-284">Когда время ожидания истекает, состояние среза меняется на TimedOut.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="1ed3b-285">delay</span><span class="sxs-lookup"><span data-stu-id="1ed3b-285">delay</span></span> |<span data-ttu-id="1ed3b-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1ed3b-286">TimeSpan</span></span> |<span data-ttu-id="1ed3b-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1ed3b-287">00:00:00</span></span> |<span data-ttu-id="1ed3b-288">Задайте задержку перед обработкой данных после начала выполнения среза.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="1ed3b-289">Действие для среза данных запускается в ожидаемое время выполнения с указанной задержкой.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="1ed3b-290">Пример: 00:10:00 (означает задержку в 10 минут).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="1ed3b-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="1ed3b-291">longRetry</span></span> |<span data-ttu-id="1ed3b-292">Целое число </span><span class="sxs-lookup"><span data-stu-id="1ed3b-292">Integer</span></span><br/><br/><span data-ttu-id="1ed3b-293">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="1ed3b-293">Max value: 10</span></span> |<span data-ttu-id="1ed3b-294">1</span><span class="sxs-lookup"><span data-stu-id="1ed3b-294">1</span></span> |<span data-ttu-id="1ed3b-295">Количество длительных повторных попыток перед завершением сбоем выполнения среза.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="1ed3b-296">Интервал между этими попытками задается свойством longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="1ed3b-297">Используйте свойство longRetry, если повторные попытки необходимо выполнять с паузами.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="1ed3b-298">Если указаны свойства Retry и longRetry, то каждая попытка longRetry включает в себя попытки Retry, и максимальное число попыток равно Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="1ed3b-299">Например, в политике действия указаны следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="1ed3b-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="1ed3b-300">Retry: 3</span></span><br/><span data-ttu-id="1ed3b-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="1ed3b-301">longRetry: 2</span></span><br/><span data-ttu-id="1ed3b-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="1ed3b-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="1ed3b-303">Предположим, что существует только один выполняемый срез (в состоянии Waiting), и каждый раз при выполнении действия происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="1ed3b-304">Первые три попытки будут выполнены подряд.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="1ed3b-305">После каждой повторной попытки срез будет находиться в состоянии Retry.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="1ed3b-306">После выполнения первых трех попыток состоянием среза станет LongRetry.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="1ed3b-307">Через час (значение свойства longRetryInterval) будут выполнены еще три попытки подряд.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="1ed3b-308">После этого состояние среза изменится на Failed и дальнейшие попытки предприниматься не будут.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="1ed3b-309">Поэтому всего было предпринято 6 попыток.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="1ed3b-310">Если какое-либо выполнение завершится успешно, то состоянием среза станет Ready и дальнейшие попытки выполняться не будут.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="1ed3b-311">Свойство longRetry можно использовать в ситуациях, когда зависимые данные поступают в неопределенное время или вся среда, в которой происходит обработка данных, непредсказуема.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="1ed3b-312">В таких случаях последовательные повторные попытки могут оказаться бесполезными, а выполненные через некоторое время, напротив, могут привести к желаемому результату.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="1ed3b-313">Предупреждение. Не задавайте высокие значения для свойств longRetry и longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="1ed3b-314">Как правило, более высокие значения приводят к появлению других системных проблем.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="1ed3b-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="1ed3b-315">longRetryInterval</span></span> |<span data-ttu-id="1ed3b-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1ed3b-316">TimeSpan</span></span> |<span data-ttu-id="1ed3b-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="1ed3b-317">00:00:00</span></span> |<span data-ttu-id="1ed3b-318">Период времени между длительными повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="1ed3b-319">Дополнительные сведения см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="1ed3b-320">Параллельная обработка срезов данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-320">Parallel processing of data slices</span></span>
<span data-ttu-id="1ed3b-321">Для конвейера можно задать прошедшую дату начала.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="1ed3b-322">При этом фабрика данных автоматически вычисляет все срезы данных из прошлого (выполняет обратное заполнение) и начинает их обработку.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="1ed3b-323">Например, если вы создадите конвейер с датой начала 2017-04-01, а текущая дата — 2017-04-10.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="1ed3b-324">Если для выходного набора данных задана ежедневная периодичность, фабрика данных начнет обработку всех срезов с 2017-04-01 по 2017-04-09 сразу, так как дата начала находится в прошлом.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="1ed3b-325">Сейчас срез за 2017-04-10 не будет обрабатываться, так как в качестве значения свойства style в разделе availability задано EndOfInterval по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="1ed3b-326">Сначала обрабатывается самый старый срез, так как значение executionPriorityOrder по умолчанию — OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="1ed3b-327">Описание свойства style см. в разделе о [доступности набора данных](#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="1ed3b-328">Описание раздела executionPriorityOrder см. в разделе о [политиках действий](#activity-policies).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="1ed3b-329">Вы можете настроить параллельную обработку срезов данных с обратным заполнением, задав свойство **concurrency** в разделе **policy** определения JSON действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="1ed3b-330">Это свойство определяет количество параллельных выполнений одного действия для обработки разных срезов.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="1ed3b-331">По умолчанию для свойства concurrency используется значение 1.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="1ed3b-332">Таким образом, по умолчанию одновременно обрабатывается один срез.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="1ed3b-333">Максимальное значение — 10.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-333">The maximum value is 10.</span></span> <span data-ttu-id="1ed3b-334">Высокое значение этого свойства ускорит обработку большого набора доступных данных в конвейере.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="1ed3b-335">Повторное выполнение невыполненного среза данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-335">Rerun a failed data slice</span></span>
<span data-ttu-id="1ed3b-336">При возникновении ошибки во время обработки среза данных можно выяснить причину сбоя, просмотрев колонки портала Azure или воспользовавшись приложением для мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="1ed3b-337">Дополнительные сведения см. в статьях [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md) и [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="1ed3b-338">Рассмотрим следующий пример, в котором показаны два действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="1ed3b-339">Activity1 и Activity2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="1ed3b-340">Activity1 использует срез Dataset1 и создает срез Dataset2, который используется в качестве входных данных в Activity2 для создания среза конечного набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![Срез, в котором произошла ошибка](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="1ed3b-342">На схеме показано, что среди трех последних срезов произошла ошибка создания среза 9–10 AM для набора данных Dataset2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="1ed3b-343">Фабрика данных автоматически отслеживает зависимости для набора данных временного ряда.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="1ed3b-344">Это задерживает запуск действия для нижестоящего среза 9-10 AM.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="1ed3b-345">Средства мониторинга и управления фабриками данных позволяют детально просмотреть журналы диагностики на предмет неудачного среза, легко найти причину неполадки и устранить ее.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="1ed3b-346">После устранения неполадки вы можете легко инициировать запуск действия для создания среза, в котором произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="1ed3b-347">Дополнительные сведения о повторных запусках, а также о переходах от одного состояния срезов данных к другому см. в статьях [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью портала Azure и PowerShell](data-factory-monitor-manage-pipelines.md) и [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="1ed3b-348">После повторного запуска среза 9–10 AM для **Dataset2**фабрика данных инициирует запуск для зависимого среза 9–10 AM в конечном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![Повторный запуск среза, в котором произошла ошибка](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="1ed3b-350">Несколько действий в конвейере</span><span class="sxs-lookup"><span data-stu-id="1ed3b-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="1ed3b-351">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="1ed3b-352">Если в конвейере несколько действий и выходные данные одного действия не являются входными данными другого, такие действия могут выполняться параллельно, при условии, что срезы входных данных для действий готовы.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="1ed3b-353">Можно объединить в цепочку два действия (выполнить одно действие вслед за другим), настроив выходной набор данных одного действия как входной набор данных другого действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1ed3b-354">Действия могут находиться в одном конвейере или разных конвейерах.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="1ed3b-355">Второе действие выполняется только после успешного завершения первого.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="1ed3b-356">Например, рассмотрим следующий случай, где конвейер содержит два действия:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="1ed3b-357">Действие A1, для которого требуется внешний входной набор данных D1. Оно создает выходной набор данных D2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="1ed3b-358">Действие A2, для которого требуется ввод из набора данных D2. Оно создает выходной набор данных D3.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="1ed3b-359">В этом сценарии действия A1 и A2 находятся в одном конвейере.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="1ed3b-360">Действие A1 выполняется, когда доступны внешние данные и достигнута запланированная частота доступности.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="1ed3b-361">Действие A2 выполняется, когда доступны запланированные срезы из D2 и достигнута запланированная частота доступности.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="1ed3b-362">В случае ошибки в одном из срезов в наборе данных D2 действие A2 не запустится для этого среза, пока он не станет доступным.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="1ed3b-363">Представление схемы с обоими действиями в одном конвейере будет выглядеть, как на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![Построение цепочки действий в одном конвейере](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="1ed3b-365">Как упоминалось ранее, действия могут находиться в разных конвейерах.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="1ed3b-366">В таком сценарии представление схемы будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![Построение цепочки действий в двух конвейерах](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="1ed3b-368">Пример см. в разделе о [последовательном копировании](#copy-sequentially) в приложении.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="1ed3b-369">Моделирование наборов данных с разной частотой</span><span class="sxs-lookup"><span data-stu-id="1ed3b-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="1ed3b-370">В примерах частота входных и выходных наборов данных и окон расписания действий была одинаковой.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="1ed3b-371">В некоторых сценариях требуется возможность создавать выходные данные с частотой, отличной от частоты одного или нескольких наборов входных данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="1ed3b-372">Фабрика данных поддерживает моделирование таких сценариев.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="1ed3b-373">Пример 1. Создание ежедневного выходного отчета по входным данным, которые доступны каждый час</span><span class="sxs-lookup"><span data-stu-id="1ed3b-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="1ed3b-374">Рассмотрим сценарий, где имеются входные данные измерений датчиков, доступные каждый час в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="1ed3b-375">Нам требуется формировать ежедневный совокупный отчет со статистикой средних, максимальных и минимальных показателей за день с помощью [действия Hive фабрики данных](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="1ed3b-376">Смоделировать этот сценарий с помощью фабрики данных можно приведенным ниже способом.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="1ed3b-377">**Входной набор данных**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-377">**Input dataset**</span></span>

<span data-ttu-id="1ed3b-378">Почасовые входные файлы за заданный день удаляются из папки.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="1ed3b-379">Для входных данных устанавливается **почасовая** доступность (frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="1ed3b-380">**Выходной набор данных**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-380">**Output dataset**</span></span>

<span data-ttu-id="1ed3b-381">Каждый день в папке создается один выходной файл за целый день.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="1ed3b-382">Для выходных данных устанавливается **ежедневная** доступность (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="1ed3b-383">**Действие: действие Hive в конвейере**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="1ed3b-384">Скрипт hive получает соответствующие сведения о *дате и времени* в качестве параметров, используя переменную **WindowStart** , как показано во фрагменте кода ниже.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="1ed3b-385">Эту переменную скрипт hive использует для загрузки данных за день из нужной папки и для создания выходных данных путем агрегирования.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
            "inputs": [
                {
                    "name": "AzureBlobInput"
                }
            ],
            "outputs": [
                {
                    "name": "AzureBlobOutput"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="1ed3b-386">На схеме ниже показан сценарий с точки зрения зависимостей данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![Зависимость данных](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="1ed3b-388">Выходной срез за каждый день зависит от 24 почасовых срезов из входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="1ed3b-389">Фабрика данных автоматически вычисляет эти зависимости, определяя срезы, которые попадают в тот же период времени, что и создаваемый выходной срез.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="1ed3b-390">Если какой-либо из 24 входных срезов недоступен, фабрика данных дожидается готовности входного среза перед запуском ежедневного действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="1ed3b-391">Пример 2. Указание зависимости с использованием выражений и функций фабрики данных</span><span class="sxs-lookup"><span data-stu-id="1ed3b-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="1ed3b-392">Рассмотрим другой сценарий.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-392">Let’s consider another scenario.</span></span> <span data-ttu-id="1ed3b-393">Предположим, есть действие Hive, которое обрабатывает два входных набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="1ed3b-394">В одном из этих наборов новые данные появляются ежедневно, а в другом — раз в неделю.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="1ed3b-395">Предположим, что требуется выполнить соединение двух входных наборов и выдать ежедневный выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="1ed3b-396">Простой подход заключается в том, чтобы фабрика данных автоматически определяла нужные входные срезы для обработки путем согласования с периодом времени выходного среза данных. Сейчас этот подход уже не работает.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="1ed3b-397">Необходимо указать фабрике данных, что для каждого действия следует использовать срез данных за последнюю неделю из еженедельного входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="1ed3b-398">Чтобы реализовать это поведение, вы используете функции фабрики данных Azure, как показано в следующем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="1ed3b-399">**Входной набор 1: большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="1ed3b-400">Первый входной набор данных представляет собой большой двоичный объект Azure, обновляемый ежедневно.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-400">The first input is the Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="1ed3b-401">**Входной набор 2: большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="1ed3b-402">Второй входной набор — большой двоичный объект Azure, обновляемый еженедельно.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-402">Input2 is the Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="1ed3b-403">**Выходной набор данных: большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-403">**Output: Azure blob**</span></span>

<span data-ttu-id="1ed3b-404">Каждый день в папке создается один выходной файл за целый день.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="1ed3b-405">Для выходных данных задается **ежедневная** доступность (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1ed3b-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="1ed3b-406">**Действие: действие Hive в конвейере**</span><span class="sxs-lookup"><span data-stu-id="1ed3b-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="1ed3b-407">Действие hive принимает два входных набора данных и создает выходной срез данных каждый день.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="1ed3b-408">Зависимость ежедневного выходного среза от входного среза предыдущей недели можно задать для еженедельных входных данных приведенным ниже образом.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="1ed3b-409">В статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md) приведен список функций и системных переменных, поддерживаемых фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="1ed3b-410">Приложение</span><span class="sxs-lookup"><span data-stu-id="1ed3b-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="1ed3b-411">Пример: последовательное копирование</span><span class="sxs-lookup"><span data-stu-id="1ed3b-411">Example: copy sequentially</span></span>
<span data-ttu-id="1ed3b-412">Несколько операций копирования можно выполнить друг за другом последовательно или упорядоченно.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="1ed3b-413">Допустим, в конвейере есть два действия копирования (CopyActivity1 и CopyActivity2) со следующими входным и выходным наборами данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="1ed3b-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="1ed3b-414">CopyActivity1</span></span>

<span data-ttu-id="1ed3b-415">Входные данные: Dataset.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-415">Input: Dataset.</span></span> <span data-ttu-id="1ed3b-416">Выходные данные: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-416">Output: Dataset2.</span></span>

<span data-ttu-id="1ed3b-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="1ed3b-417">CopyActivity2</span></span>

<span data-ttu-id="1ed3b-418">Входные данные: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-418">Input: Dataset2.</span></span>  <span data-ttu-id="1ed3b-419">Выходные данные: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-419">Output: Dataset3.</span></span>

<span data-ttu-id="1ed3b-420">Действие копирования CopyActivity2 будет выполнено только в том случае, если действие копирования CopyActivity1 прошло успешно и набор данных Dataset2 доступен.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="1ed3b-421">Ниже приведен пример файла JSON конвейера.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-421">Here is the sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob to another"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="1ed3b-422">Обратите внимание, что в примере выходной набор данных первого действия копирования (Dataset2) указан как входной набор данных второго действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="1ed3b-423">Таким образом, второе действие выполняется только после того, как готов выходной набор данных первого действия.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="1ed3b-424">В примере действие копирования CopyActivity2 может иметь другие входные данные, например набор данных Dataset3, но необходимо указать набор Dataset2 в качестве входных данных, чтобы действие копирования CopyActivity2 не запускалось, пока не завершится действие копирования CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="1ed3b-425">Например:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-425">For example:</span></span>

<span data-ttu-id="1ed3b-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="1ed3b-426">CopyActivity1</span></span>

<span data-ttu-id="1ed3b-427">Входные данные: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-427">Input: Dataset1.</span></span> <span data-ttu-id="1ed3b-428">Выходные данные: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-428">Output: Dataset2.</span></span>

<span data-ttu-id="1ed3b-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="1ed3b-429">CopyActivity2</span></span>

<span data-ttu-id="1ed3b-430">Входные данные: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="1ed3b-431">Выходные данные: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob to another"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="1ed3b-432">Обратите внимание, что в примере для второго действия копирования задано два входных набора данных.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="1ed3b-433">Если указано несколько наборов входных данных, то для копирования используется только первый набор, а другие наборы используются в качестве зависимостей.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="1ed3b-434">Действие CopyActivity2 запустится только при соблюдении следующих условий:</span><span class="sxs-lookup"><span data-stu-id="1ed3b-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="1ed3b-435">Действие CopyActivity1 успешно завершено, и набор данных Dataset2 доступен.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="1ed3b-436">Этот набор данных не используется при копировании данных в Dataset4.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="1ed3b-437">Он используется только как зависимость для планирования CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="1ed3b-438">Набор данных Dataset3 доступен.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-438">Dataset3 is available.</span></span> <span data-ttu-id="1ed3b-439">Этот данные, которые копируются в место назначения.</span><span class="sxs-lookup"><span data-stu-id="1ed3b-439">This dataset represents the data that is copied to the destination.</span></span> 