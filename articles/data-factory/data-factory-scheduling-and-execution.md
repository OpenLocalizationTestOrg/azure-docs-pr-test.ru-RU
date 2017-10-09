---
title: "aaaScheduling и выполнения с помощью фабрики данных | Документы Microsoft"
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
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="6816b-103">Планирование и исполнение с использованием фабрики данных</span><span class="sxs-lookup"><span data-stu-id="6816b-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="6816b-104">В этой статье описываются hello планированием и выполнением аспекты модели приложения hello фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="6816b-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="6816b-105">В этой статье предполагается, что вам известны основные понятия модели приложений фабрики данных: действия, конвейеры, связанные службы и наборы данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="6816b-106">Основные понятия фабрики данных Azure см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="6816b-107">Введение tooData фабрики</span><span class="sxs-lookup"><span data-stu-id="6816b-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="6816b-108">Конвейеры</span><span class="sxs-lookup"><span data-stu-id="6816b-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="6816b-109">Наборы данных</span><span class="sxs-lookup"><span data-stu-id="6816b-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="6816b-110">Время начала и окончания конвейера</span><span class="sxs-lookup"><span data-stu-id="6816b-110">Start and end times of pipeline</span></span>
<span data-ttu-id="6816b-111">Конвейер работает только в период активности, то есть между временем **начала** и **окончания**.</span><span class="sxs-lookup"><span data-stu-id="6816b-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="6816b-112">Не выполняется раньше времени начала hello или после времени окончания hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="6816b-113">Конвейер hello приостановлена, не выполняется независимо от времени его начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="6816b-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="6816b-114">Для toorun конвейера он должен быть не приостановлен.</span><span class="sxs-lookup"><span data-stu-id="6816b-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="6816b-115">В определении конвейера hello найти эти параметры (начала, окончания, приостановки):</span><span class="sxs-lookup"><span data-stu-id="6816b-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="6816b-116">Дополнительные сведения об этих свойствах см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6816b-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="6816b-117">Указание расписания для действия</span><span class="sxs-lookup"><span data-stu-id="6816b-117">Specify schedule for an activity</span></span>
<span data-ttu-id="6816b-118">Это не hello конвейера, который выполняется.</span><span class="sxs-lookup"><span data-stu-id="6816b-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="6816b-119">Это в конвейере hello hello операций, выполняемых в hello весь контекст hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="6816b-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="6816b-120">Можно указать повторяющееся расписание для действия с помощью hello **планировщика** раздел действия JSON.</span><span class="sxs-lookup"><span data-stu-id="6816b-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="6816b-121">Например можно запланировать действие toorun каждый час следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6816b-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="6816b-122">Как показано на следующая диаграмме hello, задать расписание для действия создает ряд переворачивающиеся окна с в hello конвейера начала времени и завершения.</span><span class="sxs-lookup"><span data-stu-id="6816b-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="6816b-123">"Переворачивающиеся" окна — это ряд не перекрывающихся и не соприкасающихся интервалов фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="6816b-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="6816b-124">Эти логические стыкующиеся окна для действия называются **окнами действия**.</span><span class="sxs-lookup"><span data-stu-id="6816b-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![Пример планировщика действий](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="6816b-126">Hello **планировщика** свойство для действия является необязательным.</span><span class="sxs-lookup"><span data-stu-id="6816b-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="6816b-127">При указании этого свойства должно соответствовать периодичностью hello, заданные в определении hello выходного набора данных для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="6816b-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="6816b-128">В настоящее время выходной набор данных — того, какие диски hello расписания.</span><span class="sxs-lookup"><span data-stu-id="6816b-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="6816b-129">Таким образом необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="6816b-130">Указание расписания для набора данных</span><span class="sxs-lookup"><span data-stu-id="6816b-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="6816b-131">У каждого действия в конвейере фабрики данных может быть несколько входных **наборов данных** или же ни одного, и каждое действие может производить один или несколько выходных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="6816b-132">Для действия, можно указать hello последовательность в какие hello доступна входных данных или hello выходных данных производится с помощью hello **доступности** раздела hello определения наборов данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="6816b-133">**Частота** в hello **доступности** раздел указывает единицу времени hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="6816b-134">Hello разрешенные значения для частоты: минута, час, день, неделю и месяц.</span><span class="sxs-lookup"><span data-stu-id="6816b-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="6816b-135">Hello **интервал** свойство раздела доступности hello указывает коэффициент периодичности.</span><span class="sxs-lookup"><span data-stu-id="6816b-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="6816b-136">Например: Если hello частота имеет значение tooDay и интервал too1 для выходной набор данных, hello выходных данных создаются ежедневно.</span><span class="sxs-lookup"><span data-stu-id="6816b-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="6816b-137">Если задать частоту hello минуты, рекомендуется установить интервал toono hello меньше 15.</span><span class="sxs-lookup"><span data-stu-id="6816b-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="6816b-138">В следующем примере hello, входные данные hello доступен каждый час и hello выходных данных создается каждый час (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="6816b-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="6816b-139">**Входной набор данных:**</span><span class="sxs-lookup"><span data-stu-id="6816b-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="6816b-140">**Выходной набор данных**</span><span class="sxs-lookup"><span data-stu-id="6816b-140">**Output dataset**</span></span>

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

<span data-ttu-id="6816b-141">В настоящее время **дисков hello выходного набора данных расписания**.</span><span class="sxs-lookup"><span data-stu-id="6816b-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="6816b-142">Другими словами hello расписанию, указанному для hello выходной набор данных — используется toorun действия во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="6816b-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="6816b-143">Таким образом необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="6816b-144">Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="6816b-145">В следующих hello конвейера определению hello **планировщика** свойство — используется toospecify расписание для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="6816b-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="6816b-146">Это необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="6816b-146">This property is optional.</span></span> <span data-ttu-id="6816b-147">В настоящее время hello расписание для действия "hello" должно соответствовать hello расписанием, заданным для hello выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
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

<span data-ttu-id="6816b-148">В этом примере выполняется действие hello каждый час между hello время начала и окончания hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="6816b-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="6816b-149">выходные данные Hello создается каждый час для windows трех часов (8: 00 - 9 AM, 9: 00 - 10: 00 и 10 AM - 11: 00).</span><span class="sxs-lookup"><span data-stu-id="6816b-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="6816b-150">Каждая единица данных, потребляемых или создаваемых запуском действия, называется **срезом данных**.</span><span class="sxs-lookup"><span data-stu-id="6816b-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="6816b-151">Следующая схема Hello показан пример действия с одного входного набора данных и один выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![Планировщик доступности](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="6816b-153">Hello показан hello каждый час срезы данных для hello входной и выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="6816b-154">Hello диаграмме показаны три входные срезы, готовых к обработке.</span><span class="sxs-lookup"><span data-stu-id="6816b-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="6816b-155">Действие Hello 10 11 AM идет, формирующего hello 10 11 AM вывода среза.</span><span class="sxs-lookup"><span data-stu-id="6816b-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="6816b-156">Можно получить доступ к hello интервал времени, связанные с текущей срез hello в наборе данных hello JSON с помощью переменных: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) и [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="6816b-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="6816b-157">Аналогичным образом можно получить доступ к hello интервал времени, связанные с окном действия с помощью hello WindowStart и WindowEnd.</span><span class="sxs-lookup"><span data-stu-id="6816b-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="6816b-158">расписание Hello действия должно соответствовать расписание hello hello выходного набора данных для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="6816b-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="6816b-159">Таким образом, hello SliceStart и SliceEnd значения являются hello же, как значения WindowStart и WindowEnd соответственно.</span><span class="sxs-lookup"><span data-stu-id="6816b-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="6816b-160">Дополнительные сведения об этих переменных см. в статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md#data-factory-system-variables).</span><span class="sxs-lookup"><span data-stu-id="6816b-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="6816b-161">Эти переменные можно использовать для различных целей в действии JSON.</span><span class="sxs-lookup"><span data-stu-id="6816b-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="6816b-162">Например, их можно использовать tooselect данные из входного и выходного наборов данных, представляющий временного ряда данных (например: 8 AM too9 AM).</span><span class="sxs-lookup"><span data-stu-id="6816b-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="6816b-163">В этом примере также используется **WindowStart** и **WindowEnd** tooselect необходимые данные для действия, запуска и скопируйте его tooa большой двоичный объект с hello соответствующие **folderPath**.</span><span class="sxs-lookup"><span data-stu-id="6816b-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="6816b-164">Hello **folderPath** является параметризованный toohave отдельную папку для каждого часа.</span><span class="sxs-lookup"><span data-stu-id="6816b-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="6816b-165">В предыдущих пример hello hello hello расписанием, заданным для входного и выходного наборов данных одинаковыми (каждый час).</span><span class="sxs-lookup"><span data-stu-id="6816b-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="6816b-166">Если входной набор данных для действия "hello" hello другой частотой сказать каждые 15 минут, hello действие, которое создает этот выходной набор данных по-прежнему выполняется один раз в час как hello выходной набор данных является того, какие диски hello расписание действий.</span><span class="sxs-lookup"><span data-stu-id="6816b-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="6816b-167">Дополнительные сведения см. в разделе [Моделирование наборов данных с разной частотой](#model-datasets-with-different-frequencies).</span><span class="sxs-lookup"><span data-stu-id="6816b-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="6816b-168">Доступность набора данных и политики</span><span class="sxs-lookup"><span data-stu-id="6816b-168">Dataset availability and policies</span></span>
<span data-ttu-id="6816b-169">Вы уже узнали использования hello частоту и интервал свойств в разделе доступности hello определения набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="6816b-170">Существует несколько свойств, которые влияют на hello планирования и выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="6816b-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="6816b-171">Доступность набора данных</span><span class="sxs-lookup"><span data-stu-id="6816b-171">Dataset availability</span></span> 
<span data-ttu-id="6816b-172">Hello следующей таблице описаны свойства можно использовать в hello **доступности** раздела:</span><span class="sxs-lookup"><span data-stu-id="6816b-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="6816b-173">Свойство</span><span class="sxs-lookup"><span data-stu-id="6816b-173">Property</span></span> | <span data-ttu-id="6816b-174">Описание</span><span class="sxs-lookup"><span data-stu-id="6816b-174">Description</span></span> | <span data-ttu-id="6816b-175">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6816b-175">Required</span></span> | <span data-ttu-id="6816b-176">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6816b-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6816b-177">frequency</span><span class="sxs-lookup"><span data-stu-id="6816b-177">frequency</span></span> |<span data-ttu-id="6816b-178">Указывает единицу времени hello для производственного среза набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="6816b-179"><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="6816b-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="6816b-180">Да</span><span class="sxs-lookup"><span data-stu-id="6816b-180">Yes</span></span> |<span data-ttu-id="6816b-181">Нет данных</span><span class="sxs-lookup"><span data-stu-id="6816b-181">NA</span></span> |
| <span data-ttu-id="6816b-182">interval</span><span class="sxs-lookup"><span data-stu-id="6816b-182">interval</span></span> |<span data-ttu-id="6816b-183">Задает множитель для частоты.</span><span class="sxs-lookup"><span data-stu-id="6816b-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="6816b-184">«Интервал частоты x» определяет, как часто hello срезов.</span><span class="sxs-lookup"><span data-stu-id="6816b-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="6816b-185">Если требуется hello срез в час toobe набора данных, задайте <b>частоты</b> слишком<b>час</b>, и <b>интервал</b> слишком<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="6816b-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="6816b-186"><b>Примечание</b>: Если указать для частоты минуты, рекомендуется установить интервал toono hello меньше 15</span><span class="sxs-lookup"><span data-stu-id="6816b-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="6816b-187">Да</span><span class="sxs-lookup"><span data-stu-id="6816b-187">Yes</span></span> |<span data-ttu-id="6816b-188">Нет данных</span><span class="sxs-lookup"><span data-stu-id="6816b-188">NA</span></span> |
| <span data-ttu-id="6816b-189">style</span><span class="sxs-lookup"><span data-stu-id="6816b-189">style</span></span> |<span data-ttu-id="6816b-190">Указывает, является ли hello срезов в hello начала и окончания интервала hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="6816b-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="6816b-191">StartOfInterval</span></span></li><li><span data-ttu-id="6816b-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6816b-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="6816b-193">Если частота имеет значение tooMonth и задан стиль tooEndOfInterval, hello срезов на hello последний день месяца.</span><span class="sxs-lookup"><span data-stu-id="6816b-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="6816b-194">Если задан tooStartOfInterval стиль hello, hello срезов на hello первый день месяца.</span><span class="sxs-lookup"><span data-stu-id="6816b-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="6816b-195">Если частота имеет значение tooDay и задан стиль tooEndOfInterval, hello срезов в hello последний час дня hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="6816b-196">Если частота имеет значение tooHour и задан стиль tooEndOfInterval, hello срезов в конце hello hello час.</span><span class="sxs-lookup"><span data-stu-id="6816b-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="6816b-197">Например для среза для периода с 13: 00 до 14: 00, hello срез создается в 14: 00.</span><span class="sxs-lookup"><span data-stu-id="6816b-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="6816b-198">Нет</span><span class="sxs-lookup"><span data-stu-id="6816b-198">No</span></span> |<span data-ttu-id="6816b-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6816b-199">EndOfInterval</span></span> |
| <span data-ttu-id="6816b-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="6816b-200">anchorDateTime</span></span> |<span data-ttu-id="6816b-201">Определяет hello абсолютное положение во времени, используемые границы фрагмента планировщика toocompute набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="6816b-202"><b>Примечание</b>: Если hello AnchorDateTime есть части даты, которые являются более детализированными, чем частота hello, а затем hello более детализированные части игнорируются.</span><span class="sxs-lookup"><span data-stu-id="6816b-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="6816b-203">Например, если hello <b>интервал</b> — <b>каждый час</b> (частота: час и интервал: 1) и hello <b>AnchorDateTime</b> содержит <b>минуты и секунды</b>, затем hello <b>минуты и секунды</b> части hello AnchorDateTime игнорируются.</span><span class="sxs-lookup"><span data-stu-id="6816b-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="6816b-204">Нет</span><span class="sxs-lookup"><span data-stu-id="6816b-204">No</span></span> |<span data-ttu-id="6816b-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="6816b-205">01/01/0001</span></span> |
| <span data-ttu-id="6816b-206">offset</span><span class="sxs-lookup"><span data-stu-id="6816b-206">offset</span></span> |<span data-ttu-id="6816b-207">Интервал времени, по которой hello Сдвиг начала и окончания всех фрагментов набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="6816b-208"><b>Примечание</b>: Если указаны значения для anchorDateTime и offset, результатом hello является shift hello вместе.</span><span class="sxs-lookup"><span data-stu-id="6816b-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="6816b-209">Нет</span><span class="sxs-lookup"><span data-stu-id="6816b-209">No</span></span> |<span data-ttu-id="6816b-210">Нет данных</span><span class="sxs-lookup"><span data-stu-id="6816b-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="6816b-211">Пример смещения</span><span class="sxs-lookup"><span data-stu-id="6816b-211">offset example</span></span>
<span data-ttu-id="6816b-212">По умолчанию создание ежедневных срезов (`"frequency": "Day", "interval": 1`) начинается в 00:00 (UTC).</span><span class="sxs-lookup"><span data-stu-id="6816b-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="6816b-213">Время hello начала времени toobe 6: 00 UTC вместо этого, установите hello смещение, как показано в следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="6816b-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="6816b-214">Пример для anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="6816b-214">anchorDateTime example</span></span>
<span data-ttu-id="6816b-215">В следующем примере hello hello набора данных создаются каждые 23 часа.</span><span class="sxs-lookup"><span data-stu-id="6816b-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="6816b-216">Hello первого сегмента начинается hello времени, заданного параметром anchorDateTime hello, для которого задано слишком`2017-04-19T08:00:00` (в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="6816b-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="6816b-217">Пример для Offset и Style</span><span class="sxs-lookup"><span data-stu-id="6816b-217">offset/style Example</span></span>
<span data-ttu-id="6816b-218">Hello следующий набор данных представляет собой ежемесячные набор данных и выводятся на 3-й день каждого месяца в 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="6816b-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="6816b-219">Политика набора данных</span><span class="sxs-lookup"><span data-stu-id="6816b-219">Dataset policy</span></span>
<span data-ttu-id="6816b-220">Набор данных может иметь определенные политики проверки, указывающее, как hello данные, сформированные при выполнении среза можно проверить, прежде чем он будет готов к использованию.</span><span class="sxs-lookup"><span data-stu-id="6816b-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="6816b-221">В таких случаях после завершения выполнения, срез hello состояние среза вывода hello изменяется слишком**ожидания** с подсостояния из **проверки**.</span><span class="sxs-lookup"><span data-stu-id="6816b-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="6816b-222">После проверки фрагменты hello изменяет состояние среза hello слишком**готовности**.</span><span class="sxs-lookup"><span data-stu-id="6816b-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="6816b-223">Если было произведено срез данных, но не прошел проверку hello, запуске действия для подчиненные диаграммы, которые зависят от этого среза, не обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="6816b-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="6816b-224">[Мониторинг и управление ими конвейеры](data-factory-monitor-manage-pipelines.md) деле hello различные состояния срезы данных в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="6816b-225">Hello **политики** раздела в определении набора данных, определяет условия hello или необходимо выполнить условие hello, hello фрагментов набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="6816b-226">Hello следующей таблице описаны свойства можно использовать в hello **политики** раздела:</span><span class="sxs-lookup"><span data-stu-id="6816b-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="6816b-227">Имя политики</span><span class="sxs-lookup"><span data-stu-id="6816b-227">Policy Name</span></span> | <span data-ttu-id="6816b-228">Описание</span><span class="sxs-lookup"><span data-stu-id="6816b-228">Description</span></span> | <span data-ttu-id="6816b-229">Применить слишком</span><span class="sxs-lookup"><span data-stu-id="6816b-229">Applied too</span></span>| <span data-ttu-id="6816b-230">Обязательно</span><span class="sxs-lookup"><span data-stu-id="6816b-230">Required</span></span> | <span data-ttu-id="6816b-231">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6816b-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6816b-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="6816b-232">minimumSizeMB</span></span> | <span data-ttu-id="6816b-233">Проверяет, данные hello в **BLOB-объектов Azure** соответствует hello требования минимальный размер (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="6816b-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="6816b-234">Большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="6816b-234">Azure Blob</span></span> |<span data-ttu-id="6816b-235">Нет</span><span class="sxs-lookup"><span data-stu-id="6816b-235">No</span></span> |<span data-ttu-id="6816b-236">Нет данных</span><span class="sxs-lookup"><span data-stu-id="6816b-236">NA</span></span> |
| <span data-ttu-id="6816b-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="6816b-237">minimumRows</span></span> | <span data-ttu-id="6816b-238">Проверяет, данные hello в **базы данных Azure SQL** или **таблицы Azure** содержит hello минимальное количество строк.</span><span class="sxs-lookup"><span data-stu-id="6816b-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="6816b-239">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6816b-239">Azure SQL Database</span></span></li><li><span data-ttu-id="6816b-240">таблице Azure</span><span class="sxs-lookup"><span data-stu-id="6816b-240">Azure Table</span></span></li></ul> |<span data-ttu-id="6816b-241">Нет</span><span class="sxs-lookup"><span data-stu-id="6816b-241">No</span></span> |<span data-ttu-id="6816b-242">Нет данных</span><span class="sxs-lookup"><span data-stu-id="6816b-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="6816b-243">Примеры</span><span class="sxs-lookup"><span data-stu-id="6816b-243">Examples</span></span>
<span data-ttu-id="6816b-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="6816b-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="6816b-245">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="6816b-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="6816b-246">Дополнительные сведения о наборах данных см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="6816b-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="6816b-247">Политики действий</span><span class="sxs-lookup"><span data-stu-id="6816b-247">Activity policies</span></span>
<span data-ttu-id="6816b-248">Политики влияют на поведение hello во время выполнения действия, особенно при обработке среза таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="6816b-249">Привет, в следующей таблице подробно описаны hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="6816b-250">Свойство</span><span class="sxs-lookup"><span data-stu-id="6816b-250">Property</span></span> | <span data-ttu-id="6816b-251">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="6816b-251">Permitted values</span></span> | <span data-ttu-id="6816b-252">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="6816b-252">Default Value</span></span> | <span data-ttu-id="6816b-253">Описание</span><span class="sxs-lookup"><span data-stu-id="6816b-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6816b-254">concurrency</span><span class="sxs-lookup"><span data-stu-id="6816b-254">concurrency</span></span> |<span data-ttu-id="6816b-255">Целое число </span><span class="sxs-lookup"><span data-stu-id="6816b-255">Integer</span></span> <br/><br/><span data-ttu-id="6816b-256">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="6816b-256">Max value: 10</span></span> |<span data-ttu-id="6816b-257">1</span><span class="sxs-lookup"><span data-stu-id="6816b-257">1</span></span> |<span data-ttu-id="6816b-258">Число одновременных выполнений действия hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="6816b-259">Он определяет hello число параллельных выполнений действия может произойти на различных срезах.</span><span class="sxs-lookup"><span data-stu-id="6816b-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="6816b-260">Например если действие должно toogo через большого набора данных, наличие большего значения параллелизма ускоряет обработку данных hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="6816b-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="6816b-261">executionPriorityOrder</span></span> |<span data-ttu-id="6816b-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="6816b-262">NewestFirst</span></span><br/><br/><span data-ttu-id="6816b-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="6816b-263">OldestFirst</span></span> |<span data-ttu-id="6816b-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="6816b-264">OldestFirst</span></span> |<span data-ttu-id="6816b-265">Определяет порядок hello срезы данных, которые обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="6816b-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="6816b-266">Предположим, есть два ожидающих обработки среза (от 16:00 и от 17:00).</span><span class="sxs-lookup"><span data-stu-id="6816b-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="6816b-267">При установке toobe hello executionpriorityorder значения NewestFirst сначала обрабатывается срез hello в 17: 00.</span><span class="sxs-lookup"><span data-stu-id="6816b-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="6816b-268">Аналогичным образом при установке toobe hello executionpriorityorder значения OldestFIrst затем обрабатываются срез hello в 16: 00.</span><span class="sxs-lookup"><span data-stu-id="6816b-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="6816b-269">retry</span><span class="sxs-lookup"><span data-stu-id="6816b-269">retry</span></span> |<span data-ttu-id="6816b-270">Целое число </span><span class="sxs-lookup"><span data-stu-id="6816b-270">Integer</span></span><br/><br/><span data-ttu-id="6816b-271">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="6816b-271">Max value can be 10</span></span> |<span data-ttu-id="6816b-272">0</span><span class="sxs-lookup"><span data-stu-id="6816b-272">0</span></span> |<span data-ttu-id="6816b-273">Число повторных попыток перед hello обработки данных для hello среза помечается как ошибка.</span><span class="sxs-lookup"><span data-stu-id="6816b-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="6816b-274">Выполнение действия для среза данных будет предпринята повторная попытка копирования toohello указанное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="6816b-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="6816b-275">Повторная попытка Hello выполняется как можно быстрее после сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="6816b-276">timeout</span><span class="sxs-lookup"><span data-stu-id="6816b-276">timeout</span></span> |<span data-ttu-id="6816b-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6816b-277">TimeSpan</span></span> |<span data-ttu-id="6816b-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6816b-278">00:00:00</span></span> |<span data-ttu-id="6816b-279">Время ожидания для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="6816b-279">Timeout for hello activity.</span></span> <span data-ttu-id="6816b-280">Пример: 00:10:00 (время ожидания — 10 минут).</span><span class="sxs-lookup"><span data-stu-id="6816b-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="6816b-281">Если значение не указано или равно 0, используется бесконечное время ожидания hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="6816b-282">Если hello время обработки данных среза превышает значение времени ожидания hello, отмены и hello система пытается tooretry hello обработки.</span><span class="sxs-lookup"><span data-stu-id="6816b-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="6816b-283">Hello число повторов зависит от свойства retry hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="6816b-284">При возникновении времени ожидания hello перейдет в состояние tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="6816b-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="6816b-285">delay</span><span class="sxs-lookup"><span data-stu-id="6816b-285">delay</span></span> |<span data-ttu-id="6816b-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6816b-286">TimeSpan</span></span> |<span data-ttu-id="6816b-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6816b-287">00:00:00</span></span> |<span data-ttu-id="6816b-288">Укажите задержку hello перед обработкой данных начинается срез hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="6816b-289">Hello выполнение действия для среза данных запускается после hello задержки прошлом hello ожидаемое время выполнения.</span><span class="sxs-lookup"><span data-stu-id="6816b-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="6816b-290">Пример: 00:10:00 (означает задержку в 10 минут).</span><span class="sxs-lookup"><span data-stu-id="6816b-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="6816b-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="6816b-291">longRetry</span></span> |<span data-ttu-id="6816b-292">Целое число </span><span class="sxs-lookup"><span data-stu-id="6816b-292">Integer</span></span><br/><br/><span data-ttu-id="6816b-293">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="6816b-293">Max value: 10</span></span> |<span data-ttu-id="6816b-294">1</span><span class="sxs-lookup"><span data-stu-id="6816b-294">1</span></span> |<span data-ttu-id="6816b-295">Hello количество длинных повторных попыток: hello выполнение среза завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="6816b-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="6816b-296">Интервал между этими попытками задается свойством longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="6816b-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="6816b-297">Поэтому если вам требуется toospecify время между попытками повтора, следует используйте longRetry.</span><span class="sxs-lookup"><span data-stu-id="6816b-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="6816b-298">Если указаны свойства Retry и longRetry, каждая попытка longRetry включает повторных попыток и hello максимальное число попыток повтора * longRetry.</span><span class="sxs-lookup"><span data-stu-id="6816b-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="6816b-299">Например, если у нас есть следующие параметры в политике действия hello hello:</span><span class="sxs-lookup"><span data-stu-id="6816b-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="6816b-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="6816b-300">Retry: 3</span></span><br/><span data-ttu-id="6816b-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="6816b-301">longRetry: 2</span></span><br/><span data-ttu-id="6816b-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="6816b-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="6816b-303">Предположим, что существует только один срез tooexecute (состояние ожидания) и hello действие происходит сбой выполнения каждый раз.</span><span class="sxs-lookup"><span data-stu-id="6816b-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="6816b-304">Первые три попытки будут выполнены подряд.</span><span class="sxs-lookup"><span data-stu-id="6816b-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="6816b-305">После каждой попытки hello состояние среза будет Retry.</span><span class="sxs-lookup"><span data-stu-id="6816b-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="6816b-306">После первых 3 попытки через hello состояние среза станет LongRetry.</span><span class="sxs-lookup"><span data-stu-id="6816b-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="6816b-307">Через час (значение свойства longRetryInterval) будут выполнены еще три попытки подряд.</span><span class="sxs-lookup"><span data-stu-id="6816b-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="6816b-308">После этого состояние среза hello бы сбой, и дальнейшие попытки предприниматься.</span><span class="sxs-lookup"><span data-stu-id="6816b-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="6816b-309">Поэтому всего было предпринято 6 попыток.</span><span class="sxs-lookup"><span data-stu-id="6816b-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="6816b-310">Если любое выполнение завершится успешно, hello состояние среза будет готова, и дальнейшие попытки не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="6816b-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="6816b-311">longRetry может использоваться в ситуациях, когда данные, зависящие от поступает на неопределенное время или hello общей среды подключением отображается под какие обработки данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="6816b-312">В таких случаях один за другим образом повторных попыток может не позволить и таким образом через определенные интервалы времени приводит к hello требуемого выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="6816b-313">Предупреждение. Не задавайте высокие значения для свойств longRetry и longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="6816b-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="6816b-314">Как правило, более высокие значения приводят к появлению других системных проблем.</span><span class="sxs-lookup"><span data-stu-id="6816b-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="6816b-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="6816b-315">longRetryInterval</span></span> |<span data-ttu-id="6816b-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6816b-316">TimeSpan</span></span> |<span data-ttu-id="6816b-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="6816b-317">00:00:00</span></span> |<span data-ttu-id="6816b-318">Hello задержка между попытками longretry</span><span class="sxs-lookup"><span data-stu-id="6816b-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="6816b-319">Дополнительные сведения см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="6816b-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="6816b-320">Параллельная обработка срезов данных</span><span class="sxs-lookup"><span data-stu-id="6816b-320">Parallel processing of data slices</span></span>
<span data-ttu-id="6816b-321">Можно задать hello дату начала для конвейера hello в последние hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="6816b-322">При этом фабрики данных автоматически вычисляет все срезы в прошлом hello (заливки фона) и начинает обработку их.</span><span class="sxs-lookup"><span data-stu-id="6816b-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="6816b-323">Например: Если создать конвейер с датой начала 2017 г-04-01 и hello текущая дата — 2017 г-04-10.</span><span class="sxs-lookup"><span data-stu-id="6816b-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="6816b-324">Если последовательность hello объекта hello выходной набор данных — каждый день, а затем фабрики данных начинает обработку всех фрагментов hello из 2017 г-04-01 too2017-04-09 немедленно так, как дата начала hello находится в последние hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="6816b-325">срез Hello из 2017 г-04-10 не обрабатывается еще так как значение hello свойства стиля раздела доступности hello EndOfInterval по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6816b-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="6816b-326">Hello старые срез обрабатывается сначала по умолчанию hello executionPriorityOrder равен OldestFirst.</span><span class="sxs-lookup"><span data-stu-id="6816b-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="6816b-327">Описание свойства style hello см. [доступности набора данных](#dataset-availability) раздела.</span><span class="sxs-lookup"><span data-stu-id="6816b-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="6816b-328">Описание раздела executionPriorityOrder hello см. в разделе hello [политики действий](#activity-policies) раздела.</span><span class="sxs-lookup"><span data-stu-id="6816b-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="6816b-329">Можно настроить toobe срезы данных заполнением назад параллельно обрабатываемых параметр hello **параллелизма** свойство в hello **политики** раздел действие hello JSON.</span><span class="sxs-lookup"><span data-stu-id="6816b-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="6816b-330">Это свойство определяет hello число параллельных выполнений действия может произойти на различных срезах.</span><span class="sxs-lookup"><span data-stu-id="6816b-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="6816b-331">значение свойства hello параллелизма по умолчанию Hello-1.</span><span class="sxs-lookup"><span data-stu-id="6816b-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="6816b-332">Таким образом, по умолчанию одновременно обрабатывается один срез.</span><span class="sxs-lookup"><span data-stu-id="6816b-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="6816b-333">Hello максимальное значение равно 10.</span><span class="sxs-lookup"><span data-stu-id="6816b-333">hello maximum value is 10.</span></span> <span data-ttu-id="6816b-334">Конвейера, когда потребуется toogo через большого набора данных, наличие большего значения параллелизма приводит к ускорению обработки данных hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="6816b-335">Повторное выполнение невыполненного среза данных</span><span class="sxs-lookup"><span data-stu-id="6816b-335">Rerun a failed data slice</span></span>
<span data-ttu-id="6816b-336">При возникновении ошибки во время обработки срез данных, можно выяснить причину сбоя обработки hello среза с помощью Azure портала колонках или монитора и управления приложения.</span><span class="sxs-lookup"><span data-stu-id="6816b-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="6816b-337">Дополнительные сведения см. в статьях [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md) и [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="6816b-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="6816b-338">Рассмотрим следующий пример, в котором показаны два действия hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="6816b-339">Activity1 и Activity2.</span><span class="sxs-lookup"><span data-stu-id="6816b-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="6816b-340">Activity1 использует срез Dataset1 и создает срез Dataset2, который используется в качестве ввода Activity2 tooproduce срез hello окончательного набора.</span><span class="sxs-lookup"><span data-stu-id="6816b-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![Срез, в котором произошла ошибка](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="6816b-342">Hello схемы видно, что из трех последних срезов, произошла ошибка производитель hello 9 10 AM срез для Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6816b-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="6816b-343">Фабрика данных автоматически отслеживает зависимости для набора данных для ряда времени hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="6816b-344">В результате он не запускается при выполнении среза подчиненных 9 10 AM hello hello действия.</span><span class="sxs-lookup"><span data-stu-id="6816b-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="6816b-345">Средства мониторинга и управления фабрики данных позволяют toodrill в журналы диагностики hello для hello неудачных срез tooeasily поиска hello корневой вызвать hello проблемы и устранить ее.</span><span class="sxs-lookup"><span data-stu-id="6816b-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="6816b-346">После устранения проблемы hello можно легко запустить срез неудачных hello tooproduce при выполнении действия hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="6816b-347">Дополнительные сведения о том, как toorerun и понять переходы состояний для срезов данных см. в разделе [мониторинг и управление конвейеров с помощью Azure портала колонках](data-factory-monitor-manage-pipelines.md) или [управление и мониторинг приложения](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="6816b-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="6816b-348">После повторного запуска hello 9 10 AM среза для **Dataset2**, фабрики данных запускает hello зависимых среза hello 9 10 по выполнению hello окончательного набора.</span><span class="sxs-lookup"><span data-stu-id="6816b-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![Повторный запуск среза, в котором произошла ошибка](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="6816b-350">Несколько действий в конвейере</span><span class="sxs-lookup"><span data-stu-id="6816b-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="6816b-351">Конвейер может содержать сразу несколько действий.</span><span class="sxs-lookup"><span data-stu-id="6816b-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="6816b-352">При наличии нескольких действий в конвейере и hello выходных данных действия не являются входными данными другого действия, если готовых срезы входные данные для действия hello hello действия могут выполняться параллельно.</span><span class="sxs-lookup"><span data-stu-id="6816b-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="6816b-353">Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия.</span><span class="sxs-lookup"><span data-stu-id="6816b-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="6816b-354">Hello операции могут быть в hello же конвейера или в разных конвейеров.</span><span class="sxs-lookup"><span data-stu-id="6816b-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="6816b-355">Hello второе действие выполняется, только в том случае, когда hello сначала один завершается успешно.</span><span class="sxs-lookup"><span data-stu-id="6816b-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="6816b-356">Например рассмотрим следующий случай, где содержатся два действия в конвейере hello:</span><span class="sxs-lookup"><span data-stu-id="6816b-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="6816b-357">Действие A1, для которого требуется внешний входной набор данных D1. Оно создает выходной набор данных D2.</span><span class="sxs-lookup"><span data-stu-id="6816b-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="6816b-358">Действие A2, для которого требуется ввод из набора данных D2. Оно создает выходной набор данных D3.</span><span class="sxs-lookup"><span data-stu-id="6816b-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="6816b-359">В этом сценарии, действия A1 и A2 в hello же конвейера.</span><span class="sxs-lookup"><span data-stu-id="6816b-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="6816b-360">Действие Hello запуска A1 hello внешних данных и частоты запланированных hello доступности достигается при.</span><span class="sxs-lookup"><span data-stu-id="6816b-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="6816b-361">Hello действия A2 выполняется, когда hello запланированных фрагменты из D2 становятся доступными и hello частоты запланированная доступность достигается.</span><span class="sxs-lookup"><span data-stu-id="6816b-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="6816b-362">В случае ошибки в одном из фрагментов hello в наборе данных D2 A2 не выполняется для этого среза пока она не станет доступным.</span><span class="sxs-lookup"><span data-stu-id="6816b-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="6816b-363">Здравствуйте, представление диаграммы с помощью обоих действий в hello что же конвейера выглядит следующим образом hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="6816b-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![Цепочки действий в hello же конвейера](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="6816b-365">Как упоминалось ранее, действия hello могут находиться в разных конвейеров.</span><span class="sxs-lookup"><span data-stu-id="6816b-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="6816b-366">В этом случае представление диаграммы hello выглядит следующим образом hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="6816b-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![Построение цепочки действий в двух конвейерах](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="6816b-368">. В разделе hello [скопируйте последовательно](#copy-sequentially) раздела приложение hello в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6816b-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="6816b-369">Моделирование наборов данных с разной частотой</span><span class="sxs-lookup"><span data-stu-id="6816b-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="6816b-370">В образцах hello hello частоты для входного и выходного наборов данных и hello расписание окно действия были hello же.</span><span class="sxs-lookup"><span data-stu-id="6816b-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="6816b-371">В некоторых сценариях требуется hello возможность tooproduce вывода с периодичностью, отличный от частоты hello один или несколько входных данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="6816b-372">Фабрика данных поддерживает моделирование таких сценариев.</span><span class="sxs-lookup"><span data-stu-id="6816b-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="6816b-373">Пример 1. Создание ежедневного выходного отчета по входным данным, которые доступны каждый час</span><span class="sxs-lookup"><span data-stu-id="6816b-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="6816b-374">Рассмотрим сценарий, где имеются входные данные измерений датчиков, доступные каждый час в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6816b-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="6816b-375">Вы хотите tooproduce ежедневный отчет о статистических со статистическими данными, таких как среднее, максимум и минимум hello день с [действие hive в фабрике данных](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="6816b-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="6816b-376">Смоделировать этот сценарий с помощью фабрики данных можно приведенным ниже способом.</span><span class="sxs-lookup"><span data-stu-id="6816b-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="6816b-377">**Входной набор данных**</span><span class="sxs-lookup"><span data-stu-id="6816b-377">**Input dataset**</span></span>

<span data-ttu-id="6816b-378">файлы будут удалены в папке hello для заданного дня hello каждый час входной Hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="6816b-379">Для входных данных устанавливается **почасовая** доступность (frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6816b-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="6816b-380">**Выходной набор данных**</span><span class="sxs-lookup"><span data-stu-id="6816b-380">**Output dataset**</span></span>

<span data-ttu-id="6816b-381">Один выходной файл создается каждый день в папке hello день.</span><span class="sxs-lookup"><span data-stu-id="6816b-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="6816b-382">Для выходных данных устанавливается **ежедневная** доступность (frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="6816b-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="6816b-383">**Действие: действие Hive в конвейере**</span><span class="sxs-lookup"><span data-stu-id="6816b-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="6816b-384">скрипт hive Hello принимает соответствующие hello *DateTime* сведения в качестве параметров, использующих hello **WindowStart** переменной, как показано в следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="6816b-385">скрипт hive Hello использует эти данные переменной tooload hello из требуемой папки hello день hello и выполнить выход hello toogenerate hello статистической обработки.</span><span class="sxs-lookup"><span data-stu-id="6816b-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

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

<span data-ttu-id="6816b-386">Hello следующей схеме показан сценарий hello с точки зрения зависимостей данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![Зависимость данных](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="6816b-388">срез Hello выходные данные за каждый день в зависит от 24 часам фрагменты из входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="6816b-389">Вычисляет фабрики данных, эти зависимости автоматически, изучив hello фрагменты входные данные, попадающие в hello же период времени как hello полученных toobe фрагмент выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="6816b-390">Если какой-либо входные срезы hello 24 не доступны, фабрики данных ожидает готовности перед началом выполнения действия день hello toobe ввода фрагмента hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="6816b-391">Пример 2. Указание зависимости с использованием выражений и функций фабрики данных</span><span class="sxs-lookup"><span data-stu-id="6816b-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="6816b-392">Рассмотрим другой сценарий.</span><span class="sxs-lookup"><span data-stu-id="6816b-392">Let’s consider another scenario.</span></span> <span data-ttu-id="6816b-393">Предположим, есть действие Hive, которое обрабатывает два входных набора данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="6816b-394">В одном из этих наборов новые данные появляются ежедневно, а в другом — раз в неделю.</span><span class="sxs-lookup"><span data-stu-id="6816b-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="6816b-395">Предположим, что требуется, чтобы toodo соединение между двумя входными значениями hello и формируют выходные данные каждый день.</span><span class="sxs-lookup"><span data-stu-id="6816b-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="6816b-396">Hello простой подход, в котором фабрики данных автоматически решает, правый вход hello срезы tooprocess путем выравнивания вывода toohello срез данных времени периода не работает.</span><span class="sxs-lookup"><span data-stu-id="6816b-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="6816b-397">Необходимо указать, по при выполнении каждого действия hello фабрики данных следует использовать срез данных прошлой недели для еженедельного входного набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="6816b-398">Используются функции фабрики данных Azure, как показано в следующих tooimplement фрагмент кода hello это поведение.</span><span class="sxs-lookup"><span data-stu-id="6816b-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="6816b-399">**Входной набор 1: большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="6816b-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="6816b-400">Hello сначала ввода hello BLOB-объектов Azure обновляется ежедневно.</span><span class="sxs-lookup"><span data-stu-id="6816b-400">hello first input is hello Azure blob being updated daily.</span></span>

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

<span data-ttu-id="6816b-401">**Входной набор 2: большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="6816b-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="6816b-402">Input2 — hello BLOB-объектов Azure обновляется раз в неделю.</span><span class="sxs-lookup"><span data-stu-id="6816b-402">Input2 is hello Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="6816b-403">**Выходной набор данных: большой двоичный объект Azure**</span><span class="sxs-lookup"><span data-stu-id="6816b-403">**Output: Azure blob**</span></span>

<span data-ttu-id="6816b-404">Один выходной файл создается в папке hello каждый день за день hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="6816b-405">Доступность выходных данных задано слишком**день** (частота: день, интервал: 1).</span><span class="sxs-lookup"><span data-stu-id="6816b-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="6816b-406">**Действие: действие Hive в конвейере**</span><span class="sxs-lookup"><span data-stu-id="6816b-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="6816b-407">Действие hive Hello принимает hello двух входных значений и создает выходные данные фрагмента каждый день.</span><span class="sxs-lookup"><span data-stu-id="6816b-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="6816b-408">Можно указать toodepend срез выходные данные каждый день на hello ввода фрагмента предыдущей недели для еженедельного входных данных следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6816b-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="6816b-409">В статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md) приведен список функций и системных переменных, поддерживаемых фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="6816b-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="6816b-410">Приложение</span><span class="sxs-lookup"><span data-stu-id="6816b-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="6816b-411">Пример: последовательное копирование</span><span class="sxs-lookup"><span data-stu-id="6816b-411">Example: copy sequentially</span></span>
<span data-ttu-id="6816b-412">Он является возможные toorun несколько операций копирования друг за другом в виде последовательных/упорядочены.</span><span class="sxs-lookup"><span data-stu-id="6816b-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="6816b-413">Например может иметь две копии действий в конвейере (CopyActivity1 и CopyActivity2) с hello после ввода данных выходные наборы данных:</span><span class="sxs-lookup"><span data-stu-id="6816b-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="6816b-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="6816b-414">CopyActivity1</span></span>

<span data-ttu-id="6816b-415">Входные данные: Dataset.</span><span class="sxs-lookup"><span data-stu-id="6816b-415">Input: Dataset.</span></span> <span data-ttu-id="6816b-416">Выходные данные: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6816b-416">Output: Dataset2.</span></span>

<span data-ttu-id="6816b-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="6816b-417">CopyActivity2</span></span>

<span data-ttu-id="6816b-418">Входные данные: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6816b-418">Input: Dataset2.</span></span>  <span data-ttu-id="6816b-419">Выходные данные: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="6816b-419">Output: Dataset3.</span></span>

<span data-ttu-id="6816b-420">CopyActivity2 будет выполняться только в том случае, если успешно выполнена hello CopyActivity1 и Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6816b-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="6816b-421">Ниже приведен пример hello конвейера JSON.</span><span class="sxs-lookup"><span data-stu-id="6816b-421">Here is hello sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob tooanother"
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
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="6816b-422">Обратите внимание, что в примере hello hello выходного набора данных hello первой операции копирования (Dataset2) указан в качестве входного для второго действия hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="6816b-423">Таким образом hello второе действие выполняется только в том случае, когда hello выходной набор данных из первого действия hello готов.</span><span class="sxs-lookup"><span data-stu-id="6816b-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="6816b-424">В примере hello CopyActivity2 может иметь различные данные, такие как Dataset3, но указать Dataset2 как входной tooCopyActivity2, чтобы действие hello не выполняется до завершения CopyActivity1.</span><span class="sxs-lookup"><span data-stu-id="6816b-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="6816b-425">Например:</span><span class="sxs-lookup"><span data-stu-id="6816b-425">For example:</span></span>

<span data-ttu-id="6816b-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="6816b-426">CopyActivity1</span></span>

<span data-ttu-id="6816b-427">Входные данные: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="6816b-427">Input: Dataset1.</span></span> <span data-ttu-id="6816b-428">Выходные данные: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6816b-428">Output: Dataset2.</span></span>

<span data-ttu-id="6816b-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="6816b-429">CopyActivity2</span></span>

<span data-ttu-id="6816b-430">Входные данные: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="6816b-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="6816b-431">Выходные данные: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="6816b-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob tooanother"
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
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="6816b-432">Обратите внимание, что в примере hello двух входных наборов данных указаны для второго действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="6816b-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="6816b-433">Если указано несколько входов, только hello первого входного набора данных используется для копирования данных, но другие наборы данных используются в качестве зависимости.</span><span class="sxs-lookup"><span data-stu-id="6816b-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="6816b-434">CopyActivity2 будет начинаться только после hello выполняются следующие условия:</span><span class="sxs-lookup"><span data-stu-id="6816b-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="6816b-435">Действие CopyActivity1 успешно завершено, и набор данных Dataset2 доступен.</span><span class="sxs-lookup"><span data-stu-id="6816b-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="6816b-436">Этот набор данных не используется при копировании данных tooDataset4.</span><span class="sxs-lookup"><span data-stu-id="6816b-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="6816b-437">Он используется только как зависимость для планирования CopyActivity2.</span><span class="sxs-lookup"><span data-stu-id="6816b-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="6816b-438">Набор данных Dataset3 доступен.</span><span class="sxs-lookup"><span data-stu-id="6816b-438">Dataset3 is available.</span></span> <span data-ttu-id="6816b-439">Этот набор данных представляет данные hello, скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="6816b-439">This dataset represents hello data that is copied toohello destination.</span></span> 
