---
title: "aaaAzure фабрика данных — ссылка сценария JSON | Документы Microsoft"
description: "Содержит схемы JSON для сущностей фабрики данных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="98caf-103">Справочник по написанию скриптов JSON фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="98caf-104">Эта статья содержит схемы JSON и примеры для определения сущностей фабрики данных Azure (конвейер, действие, набор данных и связанная служба).</span><span class="sxs-lookup"><span data-stu-id="98caf-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="98caf-105">Конвейер</span><span class="sxs-lookup"><span data-stu-id="98caf-105">Pipeline</span></span> 
<span data-ttu-id="98caf-106">Высокоуровневая структура Hello для определения конвейера выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="98caf-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="98caf-107">Следующей таблице описаны свойства hello в определении JSON конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="98caf-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-108">Property</span></span> | <span data-ttu-id="98caf-109">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-109">Description</span></span> | <span data-ttu-id="98caf-110">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="98caf-111">name</span><span class="sxs-lookup"><span data-stu-id="98caf-111">name</span></span> | <span data-ttu-id="98caf-112">Имя конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-112">Name of hello pipeline.</span></span> <span data-ttu-id="98caf-113">Укажите имя, которое представляет действие hello, hello действия или конвейер — настроенное toodo</span><span class="sxs-lookup"><span data-stu-id="98caf-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="98caf-114">Максимальное количество знаков: 260.</span><span class="sxs-lookup"><span data-stu-id="98caf-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="98caf-115">Должно начинаться с буквы, цифры или символа подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="98caf-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="98caf-116">Следующие знаки не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="98caf-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="98caf-117">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-117">Yes</span></span> |
| <span data-ttu-id="98caf-118">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-118">description</span></span> |<span data-ttu-id="98caf-119">Текст, описывающий, какое действие hello или конвейера используется для</span><span class="sxs-lookup"><span data-stu-id="98caf-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="98caf-120">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-120">No</span></span> |
| <span data-ttu-id="98caf-121">Действия</span><span class="sxs-lookup"><span data-stu-id="98caf-121">activities</span></span> | <span data-ttu-id="98caf-122">Содержит список действий.</span><span class="sxs-lookup"><span data-stu-id="98caf-122">Contains a list of activities.</span></span> | <span data-ttu-id="98caf-123">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-123">Yes</span></span> |
| <span data-ttu-id="98caf-124">start</span><span class="sxs-lookup"><span data-stu-id="98caf-124">start</span></span> |<span data-ttu-id="98caf-125">Дата и время начала для конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="98caf-126">Задается в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="98caf-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="98caf-127">Например: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="98caf-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="98caf-128">Это возможно toospecify местное время, например время.</span><span class="sxs-lookup"><span data-stu-id="98caf-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="98caf-129">Пример: `2016-02-27T06:00:00**-05:00`. Это 6:00 по восточному стандартному времени.</span><span class="sxs-lookup"><span data-stu-id="98caf-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="98caf-130">Hello начального и конечного свойства вместе задают активный период для конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="98caf-131">Срезы выходных данных создаются только в этот активный период.</span><span class="sxs-lookup"><span data-stu-id="98caf-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="98caf-132">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-132">No</span></span><br/><br/><span data-ttu-id="98caf-133">Если указать значение для свойства окончания hello, необходимо указать значение для свойства начала hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="98caf-134">Hello начальное и конечное время могут быть пустой toocreate конвейера.</span><span class="sxs-lookup"><span data-stu-id="98caf-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="98caf-135">Необходимо указать оба значения tooset на активный период для конвейера toorun hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="98caf-136">Если не указать время начала и окончания при создании конвейера, можно установить их позже с помощью командлета Set AzureRmDataFactoryPipelineActivePeriod hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="98caf-137">end</span><span class="sxs-lookup"><span data-stu-id="98caf-137">end</span></span> |<span data-ttu-id="98caf-138">Дата и время окончания для конвейера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="98caf-139">Не является обязательным и задается в формате ISO.</span><span class="sxs-lookup"><span data-stu-id="98caf-139">If specified must be in ISO format.</span></span> <span data-ttu-id="98caf-140">Например: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="98caf-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="98caf-141">Это возможно toospecify местное время, например время.</span><span class="sxs-lookup"><span data-stu-id="98caf-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="98caf-142">Пример: `2016-02-27T06:00:00**-05:00`. Это 6:00 по восточному стандартному времени.</span><span class="sxs-lookup"><span data-stu-id="98caf-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="98caf-143">toorun hello конвейера неопределенно долгое время, укажите 9999-09-09 как hello значение для свойства окончания hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="98caf-144">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-144">No</span></span> <br/><br/><span data-ttu-id="98caf-145">Если указать значение для свойства начала hello, необходимо указать значение для свойства окончания hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="98caf-146">См. примечания для hello **запустить** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="98caf-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="98caf-147">isPaused</span></span> |<span data-ttu-id="98caf-148">Если набор tootrue hello конвейера не выполняется.</span><span class="sxs-lookup"><span data-stu-id="98caf-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="98caf-149">Значение по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="98caf-149">Default value = false.</span></span> <span data-ttu-id="98caf-150">Можно использовать это свойство tooenable или отключить.</span><span class="sxs-lookup"><span data-stu-id="98caf-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="98caf-151">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-151">No</span></span> |
| <span data-ttu-id="98caf-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="98caf-152">pipelineMode</span></span> |<span data-ttu-id="98caf-153">метод Hello планирования выполняется для hello конвейера.</span><span class="sxs-lookup"><span data-stu-id="98caf-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="98caf-154">Допустимые значения: scheduled (по умолчанию), onetime.</span><span class="sxs-lookup"><span data-stu-id="98caf-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="98caf-155">«Запланировано» указывает, что конвейера hello запускается в заданный интервал времени в соответствии с tooits активного периода (время начала и окончания).</span><span class="sxs-lookup"><span data-stu-id="98caf-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="98caf-156">«Onetime» указывает, что этот конвейер hello запускается только один раз.</span><span class="sxs-lookup"><span data-stu-id="98caf-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="98caf-157">В настоящее время изменить или обновить однократные конвейеры после их создания нельзя.</span><span class="sxs-lookup"><span data-stu-id="98caf-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="98caf-158">Подробные сведения об однократном запуске см. в разделе [Однократный конвейер](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="98caf-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="98caf-159">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-159">No</span></span> |
| <span data-ttu-id="98caf-160">expirationTime;</span><span class="sxs-lookup"><span data-stu-id="98caf-160">expirationTime</span></span> |<span data-ttu-id="98caf-161">Продолжительность времени после создания для какой hello конвейера является допустимым и должен оставаться подготовкой.</span><span class="sxs-lookup"><span data-stu-id="98caf-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="98caf-162">Если не включает все активные сбой, или ожидающие выполнения, конвейера hello будет автоматически удалена при достижении hello время истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="98caf-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="98caf-163">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="98caf-164">Действие</span><span class="sxs-lookup"><span data-stu-id="98caf-164">Activity</span></span> 
<span data-ttu-id="98caf-165">Высокоуровневая структура Hello для действия в рамках определения конвейера (элемент действия) выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="98caf-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="98caf-166">Следующие таблицы описывают свойства hello в действии hello определения JSON.</span><span class="sxs-lookup"><span data-stu-id="98caf-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="98caf-167">Тег</span><span class="sxs-lookup"><span data-stu-id="98caf-167">Tag</span></span> | <span data-ttu-id="98caf-168">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-168">Description</span></span> | <span data-ttu-id="98caf-169">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-170">name</span><span class="sxs-lookup"><span data-stu-id="98caf-170">name</span></span> |<span data-ttu-id="98caf-171">Имя действия hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-171">Name of hello activity.</span></span> <span data-ttu-id="98caf-172">Укажите имя, которое представляет действие hello, действие hello настроить toodo</span><span class="sxs-lookup"><span data-stu-id="98caf-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="98caf-173">Максимальное количество знаков: 260.</span><span class="sxs-lookup"><span data-stu-id="98caf-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="98caf-174">Должно начинаться с буквы, цифры или символа подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="98caf-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="98caf-175">Следующие знаки не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="98caf-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="98caf-176">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-176">Yes</span></span> |
| <span data-ttu-id="98caf-177">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-177">description</span></span> |<span data-ttu-id="98caf-178">Текст, описывающий, какое действие hello используется для.</span><span class="sxs-lookup"><span data-stu-id="98caf-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="98caf-179">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-179">Yes</span></span> |
| <span data-ttu-id="98caf-180">type</span><span class="sxs-lookup"><span data-stu-id="98caf-180">type</span></span> |<span data-ttu-id="98caf-181">Указывает тип действия hello hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="98caf-182">. В разделе hello [ХРАНИЛИЩ данных](#data-stores) и [действия ПРЕОБРАЗОВАНИЯ данных](#data-transformation-activities) разделы для различных типов действий.</span><span class="sxs-lookup"><span data-stu-id="98caf-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="98caf-183">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-183">Yes</span></span> |
| <span data-ttu-id="98caf-184">inputs</span><span class="sxs-lookup"><span data-stu-id="98caf-184">inputs</span></span> |<span data-ttu-id="98caf-185">Входные таблицы, используемые действием hello</span><span class="sxs-lookup"><span data-stu-id="98caf-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="98caf-186">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-186">Yes</span></span> |
| <span data-ttu-id="98caf-187">outputs</span><span class="sxs-lookup"><span data-stu-id="98caf-187">outputs</span></span> |<span data-ttu-id="98caf-188">Выходные таблицы, используемые с действия "hello".</span><span class="sxs-lookup"><span data-stu-id="98caf-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="98caf-189">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-189">Yes</span></span> |
| <span data-ttu-id="98caf-190">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-190">linkedServiceName</span></span> |<span data-ttu-id="98caf-191">Имя hello связанной службы, используемый действием hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="98caf-192">Действие может потребоваться указать hello связаны службы, которая связывает toohello необходимые вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="98caf-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="98caf-193">Да, для действий HDInsight, Машинного обучения Azure и действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="98caf-194">Нет — для всех остальных</span><span class="sxs-lookup"><span data-stu-id="98caf-194">No for all others</span></span> |
| <span data-ttu-id="98caf-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="98caf-195">typeProperties</span></span> |<span data-ttu-id="98caf-196">Свойства в разделе "typeProperties" hello, зависят от типа действия hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="98caf-197">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-197">No</span></span> |
| <span data-ttu-id="98caf-198">policy</span><span class="sxs-lookup"><span data-stu-id="98caf-198">policy</span></span> |<span data-ttu-id="98caf-199">Политики, влияющие на поведение во время выполнения hello действия "hello".</span><span class="sxs-lookup"><span data-stu-id="98caf-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="98caf-200">Если для этого свойства не задано значение, используются стандартные политики.</span><span class="sxs-lookup"><span data-stu-id="98caf-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="98caf-201">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-201">No</span></span> |
| <span data-ttu-id="98caf-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="98caf-202">scheduler</span></span> |<span data-ttu-id="98caf-203">Свойство «планировщик» является используется toodefine требуемого планирования для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="98caf-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="98caf-204">Его подсвойства так же, как в hello hello hello [доступность свойство в наборе данных](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="98caf-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="98caf-205">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="98caf-206">Политики</span><span class="sxs-lookup"><span data-stu-id="98caf-206">Policies</span></span>
<span data-ttu-id="98caf-207">Политики влияют на поведение hello во время выполнения действия, особенно при обработке среза таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="98caf-208">Привет, в следующей таблице подробно описаны hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="98caf-209">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-209">Property</span></span> | <span data-ttu-id="98caf-210">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-210">Permitted values</span></span> | <span data-ttu-id="98caf-211">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="98caf-211">Default Value</span></span> | <span data-ttu-id="98caf-212">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-213">concurrency</span><span class="sxs-lookup"><span data-stu-id="98caf-213">concurrency</span></span> |<span data-ttu-id="98caf-214">Целое число </span><span class="sxs-lookup"><span data-stu-id="98caf-214">Integer</span></span> <br/><br/><span data-ttu-id="98caf-215">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="98caf-215">Max value: 10</span></span> |<span data-ttu-id="98caf-216">1</span><span class="sxs-lookup"><span data-stu-id="98caf-216">1</span></span> |<span data-ttu-id="98caf-217">Число одновременных выполнений действия hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="98caf-218">Он определяет hello число параллельных выполнений действия может произойти на различных срезах.</span><span class="sxs-lookup"><span data-stu-id="98caf-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="98caf-219">Например если действие должно toogo через большого набора данных, наличие большего значения параллелизма ускоряет обработку данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="98caf-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="98caf-220">executionPriorityOrder</span></span> |<span data-ttu-id="98caf-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="98caf-221">NewestFirst</span></span><br/><br/><span data-ttu-id="98caf-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="98caf-222">OldestFirst</span></span> |<span data-ttu-id="98caf-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="98caf-223">OldestFirst</span></span> |<span data-ttu-id="98caf-224">Определяет порядок hello срезы данных, которые обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="98caf-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="98caf-225">Предположим, есть два ожидающих обработки среза (от 16:00 и от 17:00).</span><span class="sxs-lookup"><span data-stu-id="98caf-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="98caf-226">При установке toobe hello executionpriorityorder значения NewestFirst сначала обрабатывается срез hello в 17: 00.</span><span class="sxs-lookup"><span data-stu-id="98caf-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="98caf-227">Аналогичным образом при установке toobe hello executionpriorityorder значения OldestFIrst затем обрабатываются срез hello в 16: 00.</span><span class="sxs-lookup"><span data-stu-id="98caf-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="98caf-228">retry</span><span class="sxs-lookup"><span data-stu-id="98caf-228">retry</span></span> |<span data-ttu-id="98caf-229">Целое число </span><span class="sxs-lookup"><span data-stu-id="98caf-229">Integer</span></span><br/><br/><span data-ttu-id="98caf-230">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="98caf-230">Max value can be 10</span></span> |<span data-ttu-id="98caf-231">0</span><span class="sxs-lookup"><span data-stu-id="98caf-231">0</span></span> |<span data-ttu-id="98caf-232">Число повторных попыток перед hello обработки данных для hello среза помечается как ошибка.</span><span class="sxs-lookup"><span data-stu-id="98caf-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="98caf-233">Выполнение действия для среза данных будет предпринята повторная попытка копирования toohello указанное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="98caf-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="98caf-234">Повторная попытка Hello выполняется как можно быстрее после сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="98caf-235">timeout</span><span class="sxs-lookup"><span data-stu-id="98caf-235">timeout</span></span> |<span data-ttu-id="98caf-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="98caf-236">TimeSpan</span></span> |<span data-ttu-id="98caf-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="98caf-237">00:00:00</span></span> |<span data-ttu-id="98caf-238">Время ожидания для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="98caf-238">Timeout for hello activity.</span></span> <span data-ttu-id="98caf-239">Пример: 00:10:00 (время ожидания — 10 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="98caf-240">Если значение не указано или равно 0, используется бесконечное время ожидания hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="98caf-241">Если hello время обработки данных среза превышает значение времени ожидания hello, отмены и hello система пытается tooretry hello обработки.</span><span class="sxs-lookup"><span data-stu-id="98caf-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="98caf-242">Hello число повторов зависит от свойства retry hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="98caf-243">При возникновении времени ожидания hello перейдет в состояние tooTimedOut.</span><span class="sxs-lookup"><span data-stu-id="98caf-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="98caf-244">delay</span><span class="sxs-lookup"><span data-stu-id="98caf-244">delay</span></span> |<span data-ttu-id="98caf-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="98caf-245">TimeSpan</span></span> |<span data-ttu-id="98caf-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="98caf-246">00:00:00</span></span> |<span data-ttu-id="98caf-247">Укажите задержку hello перед обработкой данных начинается срез hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="98caf-248">Hello выполнение действия для среза данных запускается после hello задержки прошлом hello ожидаемое время выполнения.</span><span class="sxs-lookup"><span data-stu-id="98caf-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="98caf-249">Пример: 00:10:00 (означает задержку в 10 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="98caf-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="98caf-250">longRetry</span></span> |<span data-ttu-id="98caf-251">Целое число </span><span class="sxs-lookup"><span data-stu-id="98caf-251">Integer</span></span><br/><br/><span data-ttu-id="98caf-252">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="98caf-252">Max value: 10</span></span> |<span data-ttu-id="98caf-253">1</span><span class="sxs-lookup"><span data-stu-id="98caf-253">1</span></span> |<span data-ttu-id="98caf-254">Hello количество длинных повторных попыток: hello выполнение среза завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="98caf-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="98caf-255">Интервал между этими попытками задается свойством longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="98caf-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="98caf-256">Поэтому если вам требуется toospecify время между попытками повтора, следует используйте longRetry.</span><span class="sxs-lookup"><span data-stu-id="98caf-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="98caf-257">Если указаны свойства Retry и longRetry, каждая попытка longRetry включает повторных попыток и hello максимальное число попыток повтора * longRetry.</span><span class="sxs-lookup"><span data-stu-id="98caf-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="98caf-258">Например, если у нас есть следующие параметры в политике действия hello hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="98caf-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="98caf-259">Retry: 3</span></span><br/><span data-ttu-id="98caf-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="98caf-260">longRetry: 2</span></span><br/><span data-ttu-id="98caf-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="98caf-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="98caf-262">Предположим, что существует только один срез tooexecute (состояние ожидания) и hello действие происходит сбой выполнения каждый раз.</span><span class="sxs-lookup"><span data-stu-id="98caf-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="98caf-263">Первые три попытки будут выполнены подряд.</span><span class="sxs-lookup"><span data-stu-id="98caf-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="98caf-264">После каждой попытки hello состояние среза будет Retry.</span><span class="sxs-lookup"><span data-stu-id="98caf-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="98caf-265">После первых 3 попытки через hello состояние среза станет LongRetry.</span><span class="sxs-lookup"><span data-stu-id="98caf-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="98caf-266">Через час (значение свойства longRetryInterval) будут выполнены еще три попытки подряд.</span><span class="sxs-lookup"><span data-stu-id="98caf-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="98caf-267">После этого состояние среза hello бы сбой, и дальнейшие попытки предприниматься.</span><span class="sxs-lookup"><span data-stu-id="98caf-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="98caf-268">Поэтому всего было предпринято 6 попыток.</span><span class="sxs-lookup"><span data-stu-id="98caf-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="98caf-269">Если любое выполнение завершится успешно, hello состояние среза будет готова, и дальнейшие попытки не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="98caf-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="98caf-270">longRetry может использоваться в ситуациях, когда данные, зависящие от поступает на неопределенное время или hello общей среды подключением отображается под какие обработки данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="98caf-271">В таких случаях один за другим образом повторных попыток может не позволить и таким образом через определенные интервалы времени приводит к hello требуемого выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="98caf-272">Предупреждение. Не задавайте высокие значения для свойств longRetry и longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="98caf-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="98caf-273">Как правило, более высокие значения приводят к появлению других системных проблем.</span><span class="sxs-lookup"><span data-stu-id="98caf-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="98caf-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="98caf-274">longRetryInterval</span></span> |<span data-ttu-id="98caf-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="98caf-275">TimeSpan</span></span> |<span data-ttu-id="98caf-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="98caf-276">00:00:00</span></span> |<span data-ttu-id="98caf-277">Hello задержка между попытками longretry</span><span class="sxs-lookup"><span data-stu-id="98caf-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="98caf-278">Раздел typeProperties</span><span class="sxs-lookup"><span data-stu-id="98caf-278">typeProperties section</span></span>
<span data-ttu-id="98caf-279">раздел typeProperties Hello отличается для каждого действия.</span><span class="sxs-lookup"><span data-stu-id="98caf-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="98caf-280">Преобразование действия имеют только свойства типа hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="98caf-281">В разделе [ДЕЙСТВИЯ ПРЕОБРАЗОВАНИЯ ДАННЫХ](#data-transformation-activities) этой статьи представлены примеры JSON, определяющие действия преобразования в конвейере.</span><span class="sxs-lookup"><span data-stu-id="98caf-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="98caf-282">**Действие копирования** имеет два подраздела в разделе typeProperties hello: **источника** и **приемник**.</span><span class="sxs-lookup"><span data-stu-id="98caf-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="98caf-283">В разделе [ХРАНИЛИЩ данных](#data-stores) статьи в этой статье для JSON образцы, где показано, как сохранить toouse данных в качестве источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="98caf-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="98caf-284">Пример конвейера копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-284">Sample copy pipeline</span></span>
<span data-ttu-id="98caf-285">В следующий пример конвейера hello, есть одно действие типа **копирования** в hello **действия** раздела.</span><span class="sxs-lookup"><span data-stu-id="98caf-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="98caf-286">В этом образце hello [действие копирования](data-factory-data-movement-activities.md) копирует данные из базы данных Azure SQL tooan хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="98caf-287">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="98caf-287">Note hello following points:</span></span>

* <span data-ttu-id="98caf-288">В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**.</span><span class="sxs-lookup"><span data-stu-id="98caf-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="98caf-289">Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="98caf-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="98caf-290">В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="98caf-291">В разделе [ХРАНИЛИЩ данных](#data-stores) статьи в этой статье для JSON образцы, где показано, как сохранить toouse данных в качестве источника и приемника.</span><span class="sxs-lookup"><span data-stu-id="98caf-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="98caf-292">Полное Пошаговое руководство по созданию этого конвейера, в разделе [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="98caf-293">Пример конвейера преобразования</span><span class="sxs-lookup"><span data-stu-id="98caf-293">Sample transformation pipeline</span></span>
<span data-ttu-id="98caf-294">В следующий пример конвейера hello, есть одно действие типа **HDInsightHive** в hello **действия** раздела.</span><span class="sxs-lookup"><span data-stu-id="98caf-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="98caf-295">В этом образце hello [действие Hive в HDInsight](data-factory-hive-activity.md) преобразует данные из хранилища больших двоичных объектов Azure, выполнив файл скрипта Hive в кластере Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="98caf-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
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
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="98caf-296">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="98caf-296">Note hello following points:</span></span> 

* <span data-ttu-id="98caf-297">В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="98caf-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="98caf-298">файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **AzureStorageLinkedService**) и в  **сценарий** папки в контейнере hello **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="98caf-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="98caf-299">Hello **определяет** раздел представляет параметры среды выполнения используется toospecify hello, переданных toohello скрипт hive в качестве значения конфигурации Hive (например `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="98caf-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="98caf-300">В разделе [ДЕЙСТВИЯ ПРЕОБРАЗОВАНИЯ ДАННЫХ](#data-transformation-activities) этой статьи представлены примеры JSON, определяющие действия преобразования в конвейере.</span><span class="sxs-lookup"><span data-stu-id="98caf-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="98caf-301">Полное Пошаговое руководство по созданию этого конвейера, в разделе [учебника: построение первые данные конвейера tooprocess использование кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="98caf-302">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-302">Linked service</span></span>
<span data-ttu-id="98caf-303">Высокоуровневая структура Hello для определения связанной службы выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="98caf-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="98caf-304">Следующие таблицы описывают свойства hello в действии hello определения JSON.</span><span class="sxs-lookup"><span data-stu-id="98caf-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="98caf-305">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-305">Property</span></span> | <span data-ttu-id="98caf-306">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-306">Description</span></span> | <span data-ttu-id="98caf-307">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="98caf-308">name</span><span class="sxs-lookup"><span data-stu-id="98caf-308">name</span></span> | <span data-ttu-id="98caf-309">Имя hello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-309">Name of hello linked service.</span></span> | <span data-ttu-id="98caf-310">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-310">Yes</span></span> | 
| <span data-ttu-id="98caf-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="98caf-311">properties - type</span></span> | <span data-ttu-id="98caf-312">Тип hello связанной службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-312">Type of hello linked service.</span></span> <span data-ttu-id="98caf-313">Например, служба хранилища Azure, база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="98caf-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="98caf-314">typeProperties</span></span> | <span data-ttu-id="98caf-315">раздел typeProperties Hello содержит элементы, которые различны для каждого хранилища данных или среды вычислений.</span><span class="sxs-lookup"><span data-stu-id="98caf-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="98caf-316">В разделе [хранилищ данных](#datastores) статьи для всех данных hello хранения связанных служб и [вычислений средах](#compute-environments) hello все связанные службы вычислений</span><span class="sxs-lookup"><span data-stu-id="98caf-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="98caf-317">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-317">Dataset</span></span> 
<span data-ttu-id="98caf-318">Набор данных в фабрике Azure имеет определение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="98caf-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="98caf-319">Привет, в следующей таблице описываются свойства в hello выше JSON:</span><span class="sxs-lookup"><span data-stu-id="98caf-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="98caf-320">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-320">Property</span></span> | <span data-ttu-id="98caf-321">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-321">Description</span></span> | <span data-ttu-id="98caf-322">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-322">Required</span></span> | <span data-ttu-id="98caf-323">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="98caf-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-324">name</span><span class="sxs-lookup"><span data-stu-id="98caf-324">name</span></span> | <span data-ttu-id="98caf-325">Имя набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-325">Name of hello dataset.</span></span> <span data-ttu-id="98caf-326">Правила именования для фабрики данных Azure описаны [здесь](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="98caf-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="98caf-327">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-327">Yes</span></span> |<span data-ttu-id="98caf-328">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-328">NA</span></span> |
| <span data-ttu-id="98caf-329">type</span><span class="sxs-lookup"><span data-stu-id="98caf-329">type</span></span> | <span data-ttu-id="98caf-330">Тип набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-330">Type of hello dataset.</span></span> <span data-ttu-id="98caf-331">Укажите один из типов hello, поддерживаемые фабрикой данных Azure (например: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="98caf-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="98caf-332">В разделе [ХРАНИЛИЩ данных](#data-stores) статьи для всех hello набора данных типы, поддерживаемые фабрикой данных и хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="98caf-333">structure</span><span class="sxs-lookup"><span data-stu-id="98caf-333">structure</span></span> | <span data-ttu-id="98caf-334">Схема набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-334">Schema of hello dataset.</span></span> <span data-ttu-id="98caf-335">Она содержит столбцы, их типы и т. д.</span><span class="sxs-lookup"><span data-stu-id="98caf-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="98caf-336">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-336">No</span></span> |<span data-ttu-id="98caf-337">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-337">NA</span></span> |
| <span data-ttu-id="98caf-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="98caf-338">typeProperties</span></span> | <span data-ttu-id="98caf-339">Свойства, соответствующие toohello выбранный тип.</span><span class="sxs-lookup"><span data-stu-id="98caf-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="98caf-340">В разделе [ХРАНИЛИЩА ДАННЫХ](#data-stores) указаны поддерживаемые типы и их свойства.</span><span class="sxs-lookup"><span data-stu-id="98caf-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="98caf-341">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-341">Yes</span></span> |<span data-ttu-id="98caf-342">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-342">NA</span></span> |
| <span data-ttu-id="98caf-343">external</span><span class="sxs-lookup"><span data-stu-id="98caf-343">external</span></span> | <span data-ttu-id="98caf-344">Логический флаг toospecify ли набор данных явно созданные конвейере фабрики данных или нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="98caf-345">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-345">No</span></span> |<span data-ttu-id="98caf-346">нет</span><span class="sxs-lookup"><span data-stu-id="98caf-346">false</span></span> |
| <span data-ttu-id="98caf-347">availability</span><span class="sxs-lookup"><span data-stu-id="98caf-347">availability</span></span> | <span data-ttu-id="98caf-348">Определяет hello обработки окна или hello Фрагментирование модели для производства hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="98caf-349">Дополнительные сведения о hello набора данных, Создание срезов модели см [планирования и выполнения](data-factory-scheduling-and-execution.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="98caf-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="98caf-350">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-350">Yes</span></span> |<span data-ttu-id="98caf-351">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-351">NA</span></span> |
| <span data-ttu-id="98caf-352">policy</span><span class="sxs-lookup"><span data-stu-id="98caf-352">policy</span></span> |<span data-ttu-id="98caf-353">Определяет условия hello или hello условие, которое необходимо выполнить все фрагменты hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="98caf-354">Дополнительные сведения см. в разделе [Политика наборов данных](#Policy).</span><span class="sxs-lookup"><span data-stu-id="98caf-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="98caf-355">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-355">No</span></span> |<span data-ttu-id="98caf-356">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-356">NA</span></span> |

<span data-ttu-id="98caf-357">Каждый столбец в hello **структуры** раздел содержит hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="98caf-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="98caf-358">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-358">Property</span></span> | <span data-ttu-id="98caf-359">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-359">Description</span></span> | <span data-ttu-id="98caf-360">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-361">name</span><span class="sxs-lookup"><span data-stu-id="98caf-361">name</span></span> |<span data-ttu-id="98caf-362">Имя столбца hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-362">Name of hello column.</span></span> |<span data-ttu-id="98caf-363">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-363">Yes</span></span> |
| <span data-ttu-id="98caf-364">type</span><span class="sxs-lookup"><span data-stu-id="98caf-364">type</span></span> |<span data-ttu-id="98caf-365">Тип данных столбца hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-365">Data type of hello column.</span></span>  |<span data-ttu-id="98caf-366">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-366">No</span></span> |
| <span data-ttu-id="98caf-367">culture</span><span class="sxs-lookup"><span data-stu-id="98caf-367">culture</span></span> |<span data-ttu-id="98caf-368">На базе .NET toobe языка и региональных параметров, которые используются, если указан тип и типом .NET `Datetime` или `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="98caf-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="98caf-369">Значение по умолчанию — `en-us`.</span><span class="sxs-lookup"><span data-stu-id="98caf-369">Default is `en-us`.</span></span> |<span data-ttu-id="98caf-370">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-370">No</span></span> |
| <span data-ttu-id="98caf-371">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-371">format</span></span> |<span data-ttu-id="98caf-372">Формат строки toobe используются, если указан тип и типом .NET `Datetime` или `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="98caf-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="98caf-373">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-373">No</span></span> |

<span data-ttu-id="98caf-374">В следующем примере hello, hello набор данных содержит три столбца `slicetimestamp`, `projectname`, и `pageviews` и они имеют тип: строка, строка и десятичных соответственно.</span><span class="sxs-lookup"><span data-stu-id="98caf-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="98caf-375">Hello следующей таблице описаны свойства можно использовать в hello **доступности** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="98caf-376">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-376">Property</span></span> | <span data-ttu-id="98caf-377">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-377">Description</span></span> | <span data-ttu-id="98caf-378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-378">Required</span></span> | <span data-ttu-id="98caf-379">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="98caf-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-380">frequency</span><span class="sxs-lookup"><span data-stu-id="98caf-380">frequency</span></span> |<span data-ttu-id="98caf-381">Указывает единицу времени hello для производственного среза набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="98caf-382"><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="98caf-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="98caf-383">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-383">Yes</span></span> |<span data-ttu-id="98caf-384">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-384">NA</span></span> |
| <span data-ttu-id="98caf-385">interval</span><span class="sxs-lookup"><span data-stu-id="98caf-385">interval</span></span> |<span data-ttu-id="98caf-386">Задает множитель для частоты.</span><span class="sxs-lookup"><span data-stu-id="98caf-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="98caf-387">«Интервал частоты x» определяет, как часто hello срезов.</span><span class="sxs-lookup"><span data-stu-id="98caf-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="98caf-388">Если требуется hello срез в час toobe набора данных, задайте <b>частоты</b> слишком<b>час</b>, и <b>интервал</b> слишком<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="98caf-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="98caf-389"><b>Примечание</b>: Если указать для частоты минуты, рекомендуется установить интервал toono hello меньше 15</span><span class="sxs-lookup"><span data-stu-id="98caf-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="98caf-390">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-390">Yes</span></span> |<span data-ttu-id="98caf-391">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-391">NA</span></span> |
| <span data-ttu-id="98caf-392">style</span><span class="sxs-lookup"><span data-stu-id="98caf-392">style</span></span> |<span data-ttu-id="98caf-393">Указывает, является ли hello срезов в hello начала и окончания интервала hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="98caf-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="98caf-394">StartOfInterval</span></span></li><li><span data-ttu-id="98caf-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="98caf-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="98caf-396">Если частота имеет значение tooMonth и задан стиль tooEndOfInterval, hello срезов на hello последний день месяца.</span><span class="sxs-lookup"><span data-stu-id="98caf-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="98caf-397">Если задан tooStartOfInterval стиль hello, hello срезов на hello первый день месяца.</span><span class="sxs-lookup"><span data-stu-id="98caf-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="98caf-398">Если частота имеет значение tooDay и задан стиль tooEndOfInterval, hello срезов в hello последний час дня hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="98caf-399">Если частота имеет значение tooHour и задан стиль tooEndOfInterval, hello срезов в конце hello hello час.</span><span class="sxs-lookup"><span data-stu-id="98caf-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="98caf-400">Например для среза для периода с 13: 00 до 14: 00, hello срез создается в 14: 00.</span><span class="sxs-lookup"><span data-stu-id="98caf-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="98caf-401">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-401">No</span></span> |<span data-ttu-id="98caf-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="98caf-402">EndOfInterval</span></span> |
| <span data-ttu-id="98caf-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="98caf-403">anchorDateTime</span></span> |<span data-ttu-id="98caf-404">Определяет hello абсолютное положение во времени, используемые границы фрагмента планировщика toocompute набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="98caf-405"><b>Примечание</b>: Если hello AnchorDateTime есть части даты, которые являются более детализированными, чем частота hello, а затем hello более детализированные части игнорируются.</span><span class="sxs-lookup"><span data-stu-id="98caf-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="98caf-406">Например, если hello <b>интервал</b> — <b>каждый час</b> (частота: час и интервал: 1) и hello <b>AnchorDateTime</b> содержит <b>минуты и секунды</b>затем hello <b>минуты и секунды</b> части hello AnchorDateTime игнорируются.</span><span class="sxs-lookup"><span data-stu-id="98caf-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="98caf-407">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-407">No</span></span> |<span data-ttu-id="98caf-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="98caf-408">01/01/0001</span></span> |
| <span data-ttu-id="98caf-409">offset</span><span class="sxs-lookup"><span data-stu-id="98caf-409">offset</span></span> |<span data-ttu-id="98caf-410">Интервал времени, по которой hello Сдвиг начала и окончания всех фрагментов набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="98caf-411"><b>Примечание</b>: Если указаны значения для anchorDateTime и offset, результатом hello является shift hello вместе.</span><span class="sxs-lookup"><span data-stu-id="98caf-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="98caf-412">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-412">No</span></span> |<span data-ttu-id="98caf-413">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-413">NA</span></span> |

<span data-ttu-id="98caf-414">Hello в следующем разделе доступности указывает, что hello выходной набор данных либо созданных каждый час (или) входные данные набор данных доступен каждый час:</span><span class="sxs-lookup"><span data-stu-id="98caf-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="98caf-415">Hello **политики** раздела в определении набора данных, определяет условия hello или необходимо выполнить условие hello, hello фрагментов набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="98caf-416">Имя политики</span><span class="sxs-lookup"><span data-stu-id="98caf-416">Policy Name</span></span> | <span data-ttu-id="98caf-417">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-417">Description</span></span> | <span data-ttu-id="98caf-418">Применить слишком</span><span class="sxs-lookup"><span data-stu-id="98caf-418">Applied too</span></span>| <span data-ttu-id="98caf-419">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-419">Required</span></span> | <span data-ttu-id="98caf-420">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="98caf-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="98caf-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="98caf-421">minimumSizeMB</span></span> |<span data-ttu-id="98caf-422">Проверяет, данные hello в **BLOB-объектов Azure** соответствует hello требования минимальный размер (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="98caf-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="98caf-423">Большой двоичный объект Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-423">Azure Blob</span></span> |<span data-ttu-id="98caf-424">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-424">No</span></span> |<span data-ttu-id="98caf-425">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-425">NA</span></span> |
| <span data-ttu-id="98caf-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="98caf-426">minimumRows</span></span> |<span data-ttu-id="98caf-427">Проверяет, данные hello в **базы данных Azure SQL** или **таблицы Azure** содержит hello минимальное количество строк.</span><span class="sxs-lookup"><span data-stu-id="98caf-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="98caf-428">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-428">Azure SQL Database</span></span></li><li><span data-ttu-id="98caf-429">таблице Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-429">Azure Table</span></span></li></ul> |<span data-ttu-id="98caf-430">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-430">No</span></span> |<span data-ttu-id="98caf-431">Нет данных</span><span class="sxs-lookup"><span data-stu-id="98caf-431">NA</span></span> |

<span data-ttu-id="98caf-432">**Пример**</span><span class="sxs-lookup"><span data-stu-id="98caf-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="98caf-433">Если набор данных не создается фабрикой данных Azure, он должен быть помечен как **external**.</span><span class="sxs-lookup"><span data-stu-id="98caf-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="98caf-434">Этот параметр применяется обычно toohello вводов первое действие в конвейере, если не используется действие или цепочки конвейера.</span><span class="sxs-lookup"><span data-stu-id="98caf-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="98caf-435">Имя</span><span class="sxs-lookup"><span data-stu-id="98caf-435">Name</span></span> | <span data-ttu-id="98caf-436">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-436">Description</span></span> | <span data-ttu-id="98caf-437">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-437">Required</span></span> | <span data-ttu-id="98caf-438">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="98caf-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="98caf-439">dataDelay</span></span> |<span data-ttu-id="98caf-440">Проверка времени toodelay hello на доступность hello hello внешних данных для заданного фрагмента hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="98caf-441">Например если hello данные будут доступны каждый час, hello проверка toosee hello внешних данных доступен и hello соответствующего среза с помощью dataDelay может быть задержано все готово.</span><span class="sxs-lookup"><span data-stu-id="98caf-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="98caf-442">Применяется toohello только текущее время.</span><span class="sxs-lookup"><span data-stu-id="98caf-442">Only applies toohello present time.</span></span>  <span data-ttu-id="98caf-443">Например если это 1:00 PM в данный момент, и это значение составляет 10 минут, проверки hello начинается в 13:10.</span><span class="sxs-lookup"><span data-stu-id="98caf-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="98caf-444">Этот параметр не влияет на срезы в прошлом hello (срезы со временем окончания среза + dataDelay < теперь) обрабатываются без задержки.</span><span class="sxs-lookup"><span data-stu-id="98caf-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="98caf-445">Время больше 23:59 часов необходимо с помощью hello toospecified `day.hours:minutes:seconds` формат.</span><span class="sxs-lookup"><span data-stu-id="98caf-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="98caf-446">Например toospecify 24 часа, не используйте 24:00:00; Вместо этого используйте 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="98caf-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="98caf-447">Значение 24:00:00 обозначает 24 дня (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="98caf-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="98caf-448">Чтобы задать 1 день и 4 часа, укажите 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="98caf-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="98caf-449">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-449">No</span></span> |<span data-ttu-id="98caf-450">0</span><span class="sxs-lookup"><span data-stu-id="98caf-450">0</span></span> |
| <span data-ttu-id="98caf-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="98caf-451">retryInterval</span></span> |<span data-ttu-id="98caf-452">время ожидания Hello между Далее повторной попыткой сбоя и hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="98caf-453">В случае отказа try после retryInterval могут hello следующей попытки.</span><span class="sxs-lookup"><span data-stu-id="98caf-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="98caf-454">Если это 1:00 PM прямо сейчас мы начинаем hello первой попытки.</span><span class="sxs-lookup"><span data-stu-id="98caf-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="98caf-455">Если hello длительность toocomplete hello первой проверки — 1 минута и не удалось выполнить операцию hello, hello следующий Повтор — 1:00 + 1 минута (длительность) + 1 минута (интервал повтора) = 13:02:00.</span><span class="sxs-lookup"><span data-stu-id="98caf-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="98caf-456">Срезы в прошлом hello нет без задержки.</span><span class="sxs-lookup"><span data-stu-id="98caf-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="98caf-457">Повторите попытку Hello происходит немедленно.</span><span class="sxs-lookup"><span data-stu-id="98caf-457">hello retry happens immediately.</span></span> |<span data-ttu-id="98caf-458">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-458">No</span></span> |<span data-ttu-id="98caf-459">00:01:00 (1 минута)</span><span class="sxs-lookup"><span data-stu-id="98caf-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="98caf-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-460">retryTimeout</span></span> |<span data-ttu-id="98caf-461">Здравствуйте, время ожидания для каждой повторной попытке.</span><span class="sxs-lookup"><span data-stu-id="98caf-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="98caf-462">Если это свойство имеет значение минут too10 hello toobe требованиям проверки завершена в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="98caf-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="98caf-463">Если он занимает больше 10 минут tooperform hello проверки, hello повторите истечением времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="98caf-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="98caf-464">Если все попытки проверки hello время ожидания, срез hello помечен как TimedOut.</span><span class="sxs-lookup"><span data-stu-id="98caf-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="98caf-465">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-465">No</span></span> |<span data-ttu-id="98caf-466">00:10:00 (10 минут)</span><span class="sxs-lookup"><span data-stu-id="98caf-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="98caf-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="98caf-467">maximumRetry</span></span> |<span data-ttu-id="98caf-468">Сколько раз toocheck для обеспечения доступности hello hello внешних данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="98caf-469">Hello разрешен максимальное значение равно 10.</span><span class="sxs-lookup"><span data-stu-id="98caf-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="98caf-470">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-470">No</span></span> |<span data-ttu-id="98caf-471">3</span><span class="sxs-lookup"><span data-stu-id="98caf-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="98caf-472">ХРАНИЛИЩА ДАННЫХ</span><span class="sxs-lookup"><span data-stu-id="98caf-472">DATA STORES</span></span>
<span data-ttu-id="98caf-473">Hello [связанная служба](#linked-service) раздел параметров описания для распространенных типов связанных служб tooall элементы JSON.</span><span class="sxs-lookup"><span data-stu-id="98caf-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="98caf-474">В этом разделе приводятся описания JSON элементы, которые являются определенной tooeach хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="98caf-475">Hello [Dataset](#dataset) описания раздел параметров для элементов JSON, которые существуют типы tooall наборов данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="98caf-476">В этом разделе приводятся описания JSON элементы, которые являются определенной tooeach хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="98caf-477">Hello [действия](#activity) описания раздел параметров для элементов JSON, которые существуют типы tooall действий.</span><span class="sxs-lookup"><span data-stu-id="98caf-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="98caf-478">Этот раздел предоставляет сведения об элементах JSON, которые доступны определенной tooeach хранилища данных в том случае, когда она используется в качестве источника и приемника в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="98caf-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="98caf-479">Щелкните ссылку hello hello хранилища вы заинтересованы в схемах JSON hello toosee для связанной службы, набор данных и hello источника и приемника для действия копирования hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="98caf-480">Категория</span><span class="sxs-lookup"><span data-stu-id="98caf-480">Category</span></span> | <span data-ttu-id="98caf-481">Хранилище данных</span><span class="sxs-lookup"><span data-stu-id="98caf-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="98caf-482">**Таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="98caf-482">**Azure**</span></span> |[<span data-ttu-id="98caf-483">хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="98caf-484">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="98caf-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="98caf-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="98caf-486">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="98caf-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="98caf-487">Хранилище данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="98caf-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="98caf-488">Поиск Azure;</span><span class="sxs-lookup"><span data-stu-id="98caf-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="98caf-489">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="98caf-490">**Базы данных**</span><span class="sxs-lookup"><span data-stu-id="98caf-490">**Databases**</span></span> |[<span data-ttu-id="98caf-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="98caf-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="98caf-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="98caf-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="98caf-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="98caf-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="98caf-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="98caf-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="98caf-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="98caf-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="98caf-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="98caf-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="98caf-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="98caf-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="98caf-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="98caf-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="98caf-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="98caf-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="98caf-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="98caf-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="98caf-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="98caf-501">**NoSQL**</span></span> |[<span data-ttu-id="98caf-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="98caf-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="98caf-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="98caf-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="98caf-504">**File**</span><span class="sxs-lookup"><span data-stu-id="98caf-504">**File**</span></span> |[<span data-ttu-id="98caf-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="98caf-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="98caf-506">Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="98caf-507">FTP</span><span class="sxs-lookup"><span data-stu-id="98caf-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="98caf-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="98caf-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="98caf-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="98caf-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="98caf-510">**Прочее**</span><span class="sxs-lookup"><span data-stu-id="98caf-510">**Others**</span></span> |[<span data-ttu-id="98caf-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="98caf-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="98caf-512">OData</span><span class="sxs-lookup"><span data-stu-id="98caf-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="98caf-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="98caf-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="98caf-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="98caf-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="98caf-515">Веб-таблица</span><span class="sxs-lookup"><span data-stu-id="98caf-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="98caf-516">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-517">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-517">Linked service</span></span>
<span data-ttu-id="98caf-518">Существует два типа связанных служб: связанная служба хранилища Azure и связанная служба SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="98caf-519">Связанная служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="98caf-520">toolink фабрики данных tooa учетной записи хранилища Azure с помощью hello **ключ учетной записи**, создания связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="98caf-521">Хранилище Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="98caf-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="98caf-522">Затем можно указать следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-523">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-523">Property</span></span> | <span data-ttu-id="98caf-524">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-524">Description</span></span> | <span data-ttu-id="98caf-525">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-526">connectionString</span></span> |<span data-ttu-id="98caf-527">Укажите сведения, необходимые для свойства connectionString hello tooconnect tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="98caf-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="98caf-528">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="98caf-529">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="98caf-530">Связанная служба SAS хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="98caf-531">Hello связаны SAS хранилища Azure службы позволяет toolink фабрикой данных Azure tooan учетной записи хранилища Azure с помощью подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="98caf-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="98caf-532">Он предоставляет hello фабрики данных ограничен или ограниченным временем доступа ресурсов, связанных с/tooall (/ контейнер больших двоичных объектов) в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="98caf-533">toolink фабрики данных tooa учетной записи хранилища Azure с помощью подписи общего доступа, создания службы связаны SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="98caf-534">toodefine SAS хранилища Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="98caf-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="98caf-535">Затем можно указать следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="98caf-536">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-536">Property</span></span> | <span data-ttu-id="98caf-537">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-537">Description</span></span> | <span data-ttu-id="98caf-538">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="98caf-539">sasUri</span></span> |<span data-ttu-id="98caf-540">Укажите общий URI подписи доступа toohello хранилища Azure ресурсы, такие как BLOB-объекта, контейнера или таблицы.</span><span class="sxs-lookup"><span data-stu-id="98caf-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="98caf-541">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="98caf-542">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="98caf-543">Дополнительные сведения об этих связанных службах см. в статье о [соединителе хранилища BLOB-объектов Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-544">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-544">Dataset</span></span>
<span data-ttu-id="98caf-545">toodefine набору данных больших двоичных объектов Azure hello набор **тип** hello набора данных слишком**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="98caf-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="98caf-546">Затем укажите следующие свойства конкретного BLOB-объектов Azure в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-547">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-547">Property</span></span> | <span data-ttu-id="98caf-548">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-548">Description</span></span> | <span data-ttu-id="98caf-549">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="98caf-550">folderPath</span></span> |<span data-ttu-id="98caf-551">Контейнер toohello путь к папке, в hello хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="98caf-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="98caf-552">Пример: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="98caf-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="98caf-553">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-553">Yes</span></span> |
| <span data-ttu-id="98caf-554">fileName</span><span class="sxs-lookup"><span data-stu-id="98caf-554">fileName</span></span> |<span data-ttu-id="98caf-555">Имя большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-555">Name of hello blob.</span></span> <span data-ttu-id="98caf-556">Свойство fileName является необязательным и в нем учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="98caf-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="98caf-557">При указании имени файла, hello деятельности (включая копирования) работает на hello определенным BLOB-объектом.</span><span class="sxs-lookup"><span data-stu-id="98caf-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="98caf-558">Если не указано имя файла, копирования включает все большие двоичные объекты в folderPath hello для входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="98caf-559">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл будет в следующем формате hello: данные. <Guid>.txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="98caf-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="98caf-560">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-560">No</span></span> |
| <span data-ttu-id="98caf-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="98caf-561">partitionedBy</span></span> |<span data-ttu-id="98caf-562">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="98caf-563">Можно использовать его toospecify динамического folderPath и filename для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="98caf-564">Например, путь к папке (значение folderPath) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="98caf-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="98caf-565">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-565">No</span></span> |
| <span data-ttu-id="98caf-566">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-566">format</span></span> | <span data-ttu-id="98caf-567">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-568">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-569">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-570">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-571">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-571">No</span></span> |
| <span data-ttu-id="98caf-572">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-572">compression</span></span> | <span data-ttu-id="98caf-573">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-574">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98caf-575">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-576">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-577">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-578">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-578">Example</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


<span data-ttu-id="98caf-579">Дополнительные сведения см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="98caf-580">BlobSource в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="98caf-581">При копировании данных из хранилища больших двоичных объектов Azure, задайте hello **тип источника** из hello в действии копирования слишком**BlobSource**и укажите следующие свойства в hello ** источника ** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="98caf-582">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-582">Property</span></span> | <span data-ttu-id="98caf-583">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-583">Description</span></span> | <span data-ttu-id="98caf-584">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-584">Allowed values</span></span> | <span data-ttu-id="98caf-585">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-586">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-586">recursive</span></span> |<span data-ttu-id="98caf-587">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="98caf-588">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="98caf-588">True (default value), False</span></span> |<span data-ttu-id="98caf-589">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="98caf-590">Пример: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="98caf-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="98caf-591">BlobSink в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="98caf-592">При копировании данных tooan хранилища больших двоичных объектов задайте hello **тип приемника** из hello в действии копирования слишком**BlobSink**и укажите следующие свойства в hello **приемник** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-593">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-593">Property</span></span> | <span data-ttu-id="98caf-594">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-594">Description</span></span> | <span data-ttu-id="98caf-595">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-595">Allowed values</span></span> | <span data-ttu-id="98caf-596">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="98caf-597">copyBehavior</span></span> |<span data-ttu-id="98caf-598">Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы.</span><span class="sxs-lookup"><span data-stu-id="98caf-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="98caf-599"><b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="98caf-600">Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="98caf-601"><b>FlattenHierarchy</b>: все файлы из исходной папки hello в hello сначала уровень целевую папку.</span><span class="sxs-lookup"><span data-stu-id="98caf-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="98caf-602">файлы целевой Hello иметь автоматически созданное имя.</span><span class="sxs-lookup"><span data-stu-id="98caf-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="98caf-603"><b>MergeFiles (по умолчанию):</b> объединяет все файлы из папки tooone hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="98caf-604">Если указано имя файла или большого двоичного объекта hello hello объединенный файл будет hello указанным именем. в противном случае будет автоматически формируемого имени файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="98caf-605">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="98caf-606">Пример: BlobSink</span><span class="sxs-lookup"><span data-stu-id="98caf-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-607">Дополнительные сведения см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="98caf-608">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-609">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-609">Linked service</span></span>
<span data-ttu-id="98caf-610">toodefine службы связаны хранилища Озера данных Azure, установить тип hello hello связанная служба слишком**AzureDataLakeStore**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-611">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-611">Property</span></span> | <span data-ttu-id="98caf-612">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-612">Description</span></span> | <span data-ttu-id="98caf-613">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-614">type</span><span class="sxs-lookup"><span data-stu-id="98caf-614">type</span></span> | <span data-ttu-id="98caf-615">свойство типа Hello должно быть присвоено: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="98caf-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="98caf-616">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-616">Yes</span></span> |
| <span data-ttu-id="98caf-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="98caf-617">dataLakeStoreUri</span></span> | <span data-ttu-id="98caf-618">Укажите сведения об учетной записи хранилища Озера данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="98caf-619">Он находится в hello следующий формат: `https://[accountname].azuredatalakestore.net/webhdfs/v1` или `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="98caf-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="98caf-620">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-620">Yes</span></span> |
| <span data-ttu-id="98caf-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="98caf-621">subscriptionId</span></span> | <span data-ttu-id="98caf-622">Принадлежит подписке Azure toowhich идентификатор хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="98caf-623">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="98caf-623">Required for sink</span></span> |
| <span data-ttu-id="98caf-624">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="98caf-624">resourceGroupName</span></span> | <span data-ttu-id="98caf-625">Принадлежит toowhich имя группы ресурсов Azure хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="98caf-626">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="98caf-626">Required for sink</span></span> |
| <span data-ttu-id="98caf-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="98caf-627">servicePrincipalId</span></span> | <span data-ttu-id="98caf-628">Укажите идентификатор клиента приложения hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="98caf-629">Да (для проверки подлинности на основе субъекта-службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="98caf-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="98caf-630">servicePrincipalKey</span></span> | <span data-ttu-id="98caf-631">Укажите ключ приложения hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-631">Specify hello application's key.</span></span> | <span data-ttu-id="98caf-632">Да (для проверки подлинности на основе субъекта-службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="98caf-633">tenant</span><span class="sxs-lookup"><span data-stu-id="98caf-633">tenant</span></span> | <span data-ttu-id="98caf-634">Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение.</span><span class="sxs-lookup"><span data-stu-id="98caf-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="98caf-635">Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="98caf-636">Да (для проверки подлинности на основе субъекта-службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="98caf-637">authorization</span><span class="sxs-lookup"><span data-stu-id="98caf-637">authorization</span></span> | <span data-ttu-id="98caf-638">Нажмите кнопку **авторизовать** кнопку в hello **редактор фабрики данных** и введите учетные данные, назначает свойство toothis hello автоматически созданный авторизации URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="98caf-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="98caf-639">Да (для проверки подлинности на основе учетных данных пользователя)</span><span class="sxs-lookup"><span data-stu-id="98caf-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="98caf-640">sessionid</span><span class="sxs-lookup"><span data-stu-id="98caf-640">sessionId</span></span> | <span data-ttu-id="98caf-641">Идентификатор сеанса OAuth из сеанса авторизации OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="98caf-642">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="98caf-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="98caf-643">Этот параметр создается автоматически при использовании редактора фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="98caf-644">Да (для проверки подлинности на основе учетных данных пользователя)</span><span class="sxs-lookup"><span data-stu-id="98caf-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="98caf-645">Пример: использование проверки подлинности на основе субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="98caf-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="98caf-646">Пример: использование проверки подлинности на основе учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="98caf-647">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-648">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-648">Dataset</span></span>
<span data-ttu-id="98caf-649">toodefine набор хранилища Озера данных Azure hello набор **тип** hello набора данных слишком**AzureDataLakeStore**и укажите следующие свойства в hello hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-650">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-650">Property</span></span> | <span data-ttu-id="98caf-651">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-651">Description</span></span> | <span data-ttu-id="98caf-652">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="98caf-653">folderPath</span></span> |<span data-ttu-id="98caf-654">Хранить контейнер toohello путь к папке, в hello Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="98caf-655">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-655">Yes</span></span> |
| <span data-ttu-id="98caf-656">fileName</span><span class="sxs-lookup"><span data-stu-id="98caf-656">fileName</span></span> |<span data-ttu-id="98caf-657">Имя файла hello в хранилище Озера данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="98caf-658">Свойство fileName является необязательным и в нем учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="98caf-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="98caf-659">При указании имени файла, действие hello (включая копирования) работает на конкретный файл hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="98caf-660">Если не указано имя файла, копия включает все файлы в folderPath hello для входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="98caf-661">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл будет в следующем формате hello: данные. <Guid>.txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="98caf-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="98caf-662">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-662">No</span></span> |
| <span data-ttu-id="98caf-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="98caf-663">partitionedBy</span></span> |<span data-ttu-id="98caf-664">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="98caf-665">Можно использовать его toospecify динамического folderPath и filename для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="98caf-666">Например, путь к папке (значение folderPath) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="98caf-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="98caf-667">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-667">No</span></span> |
| <span data-ttu-id="98caf-668">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-668">format</span></span> | <span data-ttu-id="98caf-669">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-670">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-671">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-672">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-673">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-673">No</span></span> |
| <span data-ttu-id="98caf-674">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-674">compression</span></span> | <span data-ttu-id="98caf-675">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-676">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98caf-677">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-678">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-679">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-680">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-681">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="98caf-682">Источник Azure Data Lake Store в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="98caf-683">При копировании данных из хранилища Озера данных Azure, задайте hello **тип источника** из hello в действии копирования слишком**AzureDataLakeStoreSource**и укажите следующие свойства в hello **источника**  раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="98caf-684">**AzureDataLakeStoreSource** поддерживает следующие свойства hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="98caf-685">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-685">Property</span></span> | <span data-ttu-id="98caf-686">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-686">Description</span></span> | <span data-ttu-id="98caf-687">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-687">Allowed values</span></span> | <span data-ttu-id="98caf-688">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-689">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-689">recursive</span></span> |<span data-ttu-id="98caf-690">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="98caf-691">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="98caf-691">True (default value), False</span></span> |<span data-ttu-id="98caf-692">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="98caf-693">Пример: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="98caf-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-694">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="98caf-695">Приемник Azure Data Lake Store в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-696">При копировании хранилища Озера данных Azure tooan данных задайте hello **тип приемника** из hello в действии копирования слишком**AzureDataLakeStoreSink**и укажите следующие свойства в hello **приемник**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-697">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-697">Property</span></span> | <span data-ttu-id="98caf-698">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-698">Description</span></span> | <span data-ttu-id="98caf-699">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-699">Allowed values</span></span> | <span data-ttu-id="98caf-700">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="98caf-701">copyBehavior</span></span> |<span data-ttu-id="98caf-702">Задает способ копирования hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="98caf-703"><b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="98caf-704">Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="98caf-705"><b>FlattenHierarchy</b>: все файлы из исходной папки hello создаются в первый уровень hello целевую папку.</span><span class="sxs-lookup"><span data-stu-id="98caf-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="98caf-706">Hello целевые файлы создаются с автоматически создаваемым именем.</span><span class="sxs-lookup"><span data-stu-id="98caf-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="98caf-707"><b>MergeFiles</b>: объединяет все файлы из папки tooone hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="98caf-708">Если указано имя файла или большого двоичного объекта hello hello объединенный файл будет hello указанным именем. в противном случае будет автоматически формируемого имени файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="98caf-709">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="98caf-710">Пример: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="98caf-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-711">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="98caf-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="98caf-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="98caf-713">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-713">Linked service</span></span>
<span data-ttu-id="98caf-714">toodefine Cosmos Azure DB связанной службы, набор hello **тип** hello связанной службы слишком**DocumentDb**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-715">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="98caf-715">**Property**</span></span> | <span data-ttu-id="98caf-716">**Описание**</span><span class="sxs-lookup"><span data-stu-id="98caf-716">**Description**</span></span> | <span data-ttu-id="98caf-717">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="98caf-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-718">connectionString</span></span> |<span data-ttu-id="98caf-719">Укажите сведения, необходимые tooconnect tooAzure Cosmos DB, базы данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="98caf-720">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-721">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="98caf-722">Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-723">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-723">Dataset</span></span>
<span data-ttu-id="98caf-724">toodefine набору данных Azure Cosmos DB hello набор **тип** hello набора данных слишком**DocumentDbCollection**и укажите следующие свойства в hello hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-725">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="98caf-725">**Property**</span></span> | <span data-ttu-id="98caf-726">**Описание**</span><span class="sxs-lookup"><span data-stu-id="98caf-726">**Description**</span></span> | <span data-ttu-id="98caf-727">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="98caf-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="98caf-728">collectionName</span></span> |<span data-ttu-id="98caf-729">Имя коллекции Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="98caf-730">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-731">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="98caf-732">Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="98caf-733">Источник коллекции Azure Cosmos DB в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="98caf-734">При копировании данных из базы данных Cosmos Azure задайте hello **тип источника** из hello в действии копирования слишком**DocumentDbCollectionSource**и укажите следующие свойства в hello **источника** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-735">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="98caf-735">**Property**</span></span> | <span data-ttu-id="98caf-736">**Описание**</span><span class="sxs-lookup"><span data-stu-id="98caf-736">**Description**</span></span> | <span data-ttu-id="98caf-737">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="98caf-737">**Allowed values**</span></span> | <span data-ttu-id="98caf-738">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="98caf-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-739">query</span><span class="sxs-lookup"><span data-stu-id="98caf-739">query</span></span> |<span data-ttu-id="98caf-740">Укажите данные tooread hello запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="98caf-741">Строка запроса, поддерживаемая Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="98caf-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="98caf-742">Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="98caf-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="98caf-743">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-743">No</span></span> <br/><br/><span data-ttu-id="98caf-744">Если не указан, hello выполняемой инструкции SQL:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="98caf-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="98caf-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="98caf-745">nestingSeparator</span></span> |<span data-ttu-id="98caf-746">Вложенные tooindicate специальный символ, который hello документа</span><span class="sxs-lookup"><span data-stu-id="98caf-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="98caf-747">Любой символ.</span><span class="sxs-lookup"><span data-stu-id="98caf-747">Any character.</span></span> <br/><br/><span data-ttu-id="98caf-748">Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="98caf-749">Фабрика данных Azure позволяет пользовательская иерархия toodenote через nestingSeparator, который является «.»</span><span class="sxs-lookup"><span data-stu-id="98caf-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="98caf-750">в hello выше примерах.</span><span class="sxs-lookup"><span data-stu-id="98caf-750">in hello above examples.</span></span> <span data-ttu-id="98caf-751">Разделитель hello hello действие копирования будет создавать объект «Name» hello с тремя дочерние элементы первой, средней и Last, соответствующим too"Name.First», «Name.Middle» и «Name.Last» в hello определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="98caf-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="98caf-752">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-753">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="98caf-754">Приемник коллекции Azure Cosmos DB в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-755">При копировании данных tooAzure Cosmos DB задать hello **тип приемника** из hello в действии копирования слишком**DocumentDbCollectionSink**и укажите следующие свойства в hello **приемник**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-756">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="98caf-756">**Property**</span></span> | <span data-ttu-id="98caf-757">**Описание**</span><span class="sxs-lookup"><span data-stu-id="98caf-757">**Description**</span></span> | <span data-ttu-id="98caf-758">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="98caf-758">**Allowed values**</span></span> | <span data-ttu-id="98caf-759">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="98caf-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="98caf-760">nestingSeparator</span></span> |<span data-ttu-id="98caf-761">Требуется специальный символ в tooindicate имя столбца источника hello вложенном документе.</span><span class="sxs-lookup"><span data-stu-id="98caf-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="98caf-762">Пример выше: `Name.First` в выходных данных hello таблицы выводятся hello следующая структура JSON в документе Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="98caf-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="98caf-763">"Name": {</span></span><br/>    <span data-ttu-id="98caf-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="98caf-764">"First": "John"</span></span><br/><span data-ttu-id="98caf-765">},</span><span class="sxs-lookup"><span data-stu-id="98caf-765">},</span></span> |<span data-ttu-id="98caf-766">Символ, используемые tooseparate уровней вложения.</span><span class="sxs-lookup"><span data-stu-id="98caf-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="98caf-767">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="98caf-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="98caf-768">Символ, используемые tooseparate уровней вложения.</span><span class="sxs-lookup"><span data-stu-id="98caf-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="98caf-769">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="98caf-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="98caf-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-770">writeBatchSize</span></span> |<span data-ttu-id="98caf-771">Число используемых параллельных запросов документов toocreate tooAzure Cosmos DB службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="98caf-772">Можно оптимизировать производительность hello, при копировании данных из базы данных Azure Cosmos при помощи этого свойства.</span><span class="sxs-lookup"><span data-stu-id="98caf-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="98caf-773">При увеличении writeBatchSize, так как несколько параллельных запросов tooAzure Cosmos DB отправляются можно ожидать более высокую производительность.</span><span class="sxs-lookup"><span data-stu-id="98caf-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="98caf-774">Тем не менее необходимо tooavoid регулирования, может вызывать ошибки приветственное сообщение: «частота велик» запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="98caf-775">Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования, можно использовать доступной пропускной способностью большинство лучше hello toohave коллекции (например, S3) (2 500 запрос единицы в секунду).</span><span class="sxs-lookup"><span data-stu-id="98caf-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="98caf-776">Целое число </span><span class="sxs-lookup"><span data-stu-id="98caf-776">Integer</span></span> |<span data-ttu-id="98caf-777">Нет (значение по умолчанию — 5)</span><span class="sxs-lookup"><span data-stu-id="98caf-777">No (default: 5)</span></span> |
| <span data-ttu-id="98caf-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-778">writeBatchTimeout</span></span> |<span data-ttu-id="98caf-779">Время ожидания для операции toocomplete hello до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="98caf-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="98caf-780">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="98caf-780">timespan</span></span><br/><br/> <span data-ttu-id="98caf-781">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="98caf-782">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-783">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="98caf-784">Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="98caf-785">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-786">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-786">Linked service</span></span>
<span data-ttu-id="98caf-787">toodefine базы данных SQL Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDatabase**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-788">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-788">Property</span></span> | <span data-ttu-id="98caf-789">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-789">Description</span></span> | <span data-ttu-id="98caf-790">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-791">connectionString</span></span> |<span data-ttu-id="98caf-792">Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных SQL Azure toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="98caf-793">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-794">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="98caf-795">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-796">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-796">Dataset</span></span>
<span data-ttu-id="98caf-797">toodefine набор данных базы данных SQL Azure, набор hello **тип** hello набора данных слишком**AzureSqlTable**и укажите следующие свойства в hello hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-798">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-798">Property</span></span> | <span data-ttu-id="98caf-799">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-799">Description</span></span> | <span data-ttu-id="98caf-800">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-801">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-801">tableName</span></span> |<span data-ttu-id="98caf-802">Имя hello таблицы или представления в экземпляр базы данных SQL Azure hello, связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="98caf-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="98caf-803">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-804">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="98caf-805">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="98caf-806">Источник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="98caf-807">При копировании данных из базы данных SQL Azure, задайте hello **тип источника** из hello в действии копирования слишком**SqlSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-808">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-808">Property</span></span> | <span data-ttu-id="98caf-809">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-809">Description</span></span> | <span data-ttu-id="98caf-810">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-810">Allowed values</span></span> | <span data-ttu-id="98caf-811">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="98caf-812">sqlReaderQuery</span></span> |<span data-ttu-id="98caf-813">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-814">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-814">SQL query string.</span></span> <span data-ttu-id="98caf-815">Пример: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-816">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-816">No</span></span> |
| <span data-ttu-id="98caf-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="98caf-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="98caf-818">Имя hello хранимой процедуры, который считывает данные из таблицы источника hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="98caf-819">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="98caf-820">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-820">No</span></span> |
| <span data-ttu-id="98caf-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-821">storedProcedureParameters</span></span> |<span data-ttu-id="98caf-822">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="98caf-823">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-823">Name/value pairs.</span></span> <span data-ttu-id="98caf-824">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="98caf-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="98caf-825">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-826">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="98caf-827">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="98caf-828">Приемник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-829">При копировании данных tooAzure базы данных SQL, задайте hello **тип приемника** из hello в действии копирования слишком**SqlSink**и укажите следующие свойства в hello **приемник** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-830">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-830">Property</span></span> | <span data-ttu-id="98caf-831">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-831">Description</span></span> | <span data-ttu-id="98caf-832">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-832">Allowed values</span></span> | <span data-ttu-id="98caf-833">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-834">writeBatchTimeout</span></span> |<span data-ttu-id="98caf-835">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="98caf-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="98caf-836">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="98caf-836">timespan</span></span><br/><br/> <span data-ttu-id="98caf-837">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="98caf-838">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-838">No</span></span> |
| <span data-ttu-id="98caf-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-839">writeBatchSize</span></span> |<span data-ttu-id="98caf-840">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="98caf-841">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="98caf-841">Integer (number of rows)</span></span> |<span data-ttu-id="98caf-842">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="98caf-842">No (default: 10000)</span></span> |
| <span data-ttu-id="98caf-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="98caf-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="98caf-844">Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="98caf-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="98caf-845">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-845">A query statement.</span></span> |<span data-ttu-id="98caf-846">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-846">No</span></span> |
| <span data-ttu-id="98caf-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="98caf-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="98caf-848">Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="98caf-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="98caf-849">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="98caf-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="98caf-850">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-850">No</span></span> |
| <span data-ttu-id="98caf-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="98caf-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="98caf-852">Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="98caf-853">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="98caf-854">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-854">No</span></span> |
| <span data-ttu-id="98caf-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-855">storedProcedureParameters</span></span> |<span data-ttu-id="98caf-856">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="98caf-857">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-857">Name/value pairs.</span></span> <span data-ttu-id="98caf-858">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="98caf-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="98caf-859">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-859">No</span></span> |
| <span data-ttu-id="98caf-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="98caf-860">sqlWriterTableType</span></span> |<span data-ttu-id="98caf-861">Укажите имя toobe тип таблицы, используемых в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="98caf-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="98caf-862">Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей.</span><span class="sxs-lookup"><span data-stu-id="98caf-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="98caf-863">Кода хранимой процедуры можно объединять hello данные копируются с существующими данными.</span><span class="sxs-lookup"><span data-stu-id="98caf-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="98caf-864">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="98caf-864">A table type name.</span></span> |<span data-ttu-id="98caf-865">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-866">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-867">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="98caf-868">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-869">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-869">Linked service</span></span>
<span data-ttu-id="98caf-870">Хранилище данных SQL Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDW**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-871">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-871">Property</span></span> | <span data-ttu-id="98caf-872">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-872">Description</span></span> | <span data-ttu-id="98caf-873">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-874">connectionString</span></span> |<span data-ttu-id="98caf-875">Укажите сведения, необходимые для свойства connectionString hello tooconnect toohello хранилище данных SQL Azure экземпляра.</span><span class="sxs-lookup"><span data-stu-id="98caf-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="98caf-876">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="98caf-877">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="98caf-878">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-879">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-879">Dataset</span></span>
<span data-ttu-id="98caf-880">toodefine набор данных хранилище данных SQL Azure, набор hello **тип** hello набора данных слишком**AzureSqlDWTable**и укажите следующие свойства в hello hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-881">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-881">Property</span></span> | <span data-ttu-id="98caf-882">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-882">Description</span></span> | <span data-ttu-id="98caf-883">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-884">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-884">tableName</span></span> |<span data-ttu-id="98caf-885">Имя hello таблицы или представления в базе данных хранилища данных SQL Azure hello, hello связанной службы относится.</span><span class="sxs-lookup"><span data-stu-id="98caf-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="98caf-886">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-887">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-888">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="98caf-889">Источник хранилища данных SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="98caf-890">При копировании данных из хранилища данных SQL Azure, задайте hello **тип источника** из hello в действии копирования слишком**SqlDWSource**и укажите следующие свойства в hello **источника**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-891">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-891">Property</span></span> | <span data-ttu-id="98caf-892">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-892">Description</span></span> | <span data-ttu-id="98caf-893">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-893">Allowed values</span></span> | <span data-ttu-id="98caf-894">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="98caf-895">sqlReaderQuery</span></span> |<span data-ttu-id="98caf-896">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-897">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-897">SQL query string.</span></span> <span data-ttu-id="98caf-898">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-899">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-899">No</span></span> |
| <span data-ttu-id="98caf-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="98caf-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="98caf-901">Имя hello хранимой процедуры, который считывает данные из таблицы источника hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="98caf-902">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="98caf-903">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-903">No</span></span> |
| <span data-ttu-id="98caf-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-904">storedProcedureParameters</span></span> |<span data-ttu-id="98caf-905">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="98caf-906">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-906">Name/value pairs.</span></span> <span data-ttu-id="98caf-907">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="98caf-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="98caf-908">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-909">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-910">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="98caf-911">Приемник хранилища данных SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-912">При копировании данных tooAzure хранилище данных SQL, задайте hello **тип приемника** из hello в действии копирования слишком**SqlDWSink**и укажите следующие свойства в hello **приемник** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-913">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-913">Property</span></span> | <span data-ttu-id="98caf-914">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-914">Description</span></span> | <span data-ttu-id="98caf-915">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-915">Allowed values</span></span> | <span data-ttu-id="98caf-916">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="98caf-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="98caf-918">Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="98caf-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="98caf-919">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-919">A query statement.</span></span> |<span data-ttu-id="98caf-920">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-920">No</span></span> |
| <span data-ttu-id="98caf-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="98caf-921">allowPolyBase</span></span> |<span data-ttu-id="98caf-922">Указывает, является ли toouse PolyBase (если применимо), а не BULKINSERT механизм.</span><span class="sxs-lookup"><span data-stu-id="98caf-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="98caf-923">**С помощью PolyBase — hello рекомендуется как tooload данные в хранилище данных SQL.**</span><span class="sxs-lookup"><span data-stu-id="98caf-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="98caf-924">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-924">True</span></span> <br/><span data-ttu-id="98caf-925">False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-925">False (default)</span></span> |<span data-ttu-id="98caf-926">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-926">No</span></span> |
| <span data-ttu-id="98caf-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="98caf-927">polyBaseSettings</span></span> |<span data-ttu-id="98caf-928">Группа свойств, которые могут быть указаны при hello **allowPolybase** задано слишком**true**.</span><span class="sxs-lookup"><span data-stu-id="98caf-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="98caf-929">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-929">No</span></span> |
| <span data-ttu-id="98caf-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="98caf-930">rejectValue</span></span> |<span data-ttu-id="98caf-931">Указывает hello число или процент строк, может быть отклонено перед hello запрос завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="98caf-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="98caf-932">Узнайте больше о hello PolyBase отклонить параметры в hello **аргументы** раздел [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="98caf-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="98caf-933">0 (по умолчанию), 1, 2, ...</span><span class="sxs-lookup"><span data-stu-id="98caf-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="98caf-934">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-934">No</span></span> |
| <span data-ttu-id="98caf-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="98caf-935">rejectType</span></span> |<span data-ttu-id="98caf-936">Указывает, задан ли параметр rejectValue hello в значение литерала или в процентах.</span><span class="sxs-lookup"><span data-stu-id="98caf-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="98caf-937">Value (по умолчанию), Percentage</span><span class="sxs-lookup"><span data-stu-id="98caf-937">Value (default), Percentage</span></span> |<span data-ttu-id="98caf-938">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-938">No</span></span> |
| <span data-ttu-id="98caf-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="98caf-939">rejectSampleValue</span></span> |<span data-ttu-id="98caf-940">Определяет количество hello tooretrieve строк перед hello PolyBase повторно вычисляет процент отклоненных строк hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="98caf-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="98caf-941">1, 2, …</span></span> |<span data-ttu-id="98caf-942">Да, если **rejectType** имеет значение **percentage**.</span><span class="sxs-lookup"><span data-stu-id="98caf-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="98caf-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="98caf-943">useTypeDefault</span></span> |<span data-ttu-id="98caf-944">Указывает, как toohandle отсутствующих значений в разделенных текстовых файлов, если PolyBase получает данные из текстового файла hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="98caf-945">Дополнительные сведения об этом свойстве из подраздела аргументы hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="98caf-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="98caf-946">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-946">True, False (default)</span></span> |<span data-ttu-id="98caf-947">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-947">No</span></span> |
| <span data-ttu-id="98caf-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-948">writeBatchSize</span></span> |<span data-ttu-id="98caf-949">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello</span><span class="sxs-lookup"><span data-stu-id="98caf-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="98caf-950">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="98caf-950">Integer (number of rows)</span></span> |<span data-ttu-id="98caf-951">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="98caf-951">No (default: 10000)</span></span> |
| <span data-ttu-id="98caf-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-952">writeBatchTimeout</span></span> |<span data-ttu-id="98caf-953">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="98caf-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="98caf-954">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="98caf-954">timespan</span></span><br/><br/> <span data-ttu-id="98caf-955">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="98caf-956">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-957">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-958">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="98caf-959">поиск Azure;</span><span class="sxs-lookup"><span data-stu-id="98caf-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-960">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-960">Linked service</span></span>
<span data-ttu-id="98caf-961">toodefine поиска Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureSearch**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-962">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-962">Property</span></span> | <span data-ttu-id="98caf-963">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-963">Description</span></span> | <span data-ttu-id="98caf-964">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="98caf-965">url</span><span class="sxs-lookup"><span data-stu-id="98caf-965">url</span></span> | <span data-ttu-id="98caf-966">URL-адрес для службы поиска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="98caf-967">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-967">Yes</span></span> |
| <span data-ttu-id="98caf-968">key</span><span class="sxs-lookup"><span data-stu-id="98caf-968">key</span></span> | <span data-ttu-id="98caf-969">Ключ администратора для hello службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="98caf-970">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-971">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="98caf-972">Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-973">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-973">Dataset</span></span>
<span data-ttu-id="98caf-974">toodefine набор данных поиска Azure, набор hello **тип** hello набора данных слишком**AzureSearchIndex**и укажите следующие свойства в hello hello **typeProperties** раздела :</span><span class="sxs-lookup"><span data-stu-id="98caf-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-975">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-975">Property</span></span> | <span data-ttu-id="98caf-976">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-976">Description</span></span> | <span data-ttu-id="98caf-977">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="98caf-978">type</span><span class="sxs-lookup"><span data-stu-id="98caf-978">type</span></span> | <span data-ttu-id="98caf-979">свойство типа Hello должно быть задано слишком**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="98caf-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="98caf-980">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-980">Yes</span></span> |
| <span data-ttu-id="98caf-981">indexName</span><span class="sxs-lookup"><span data-stu-id="98caf-981">indexName</span></span> | <span data-ttu-id="98caf-982">Имя индекса поиска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="98caf-983">Фабрика данных hello индекс не создается.</span><span class="sxs-lookup"><span data-stu-id="98caf-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="98caf-984">Hello индекс должен существовать в поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="98caf-985">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-986">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="98caf-987">Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="98caf-988">Приемник индекса Поиска Azure в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-989">При копировании данных индекс поиска Azure tooan задать hello **тип приемника** из hello в действии копирования слишком**AzureSearchIndexSink**и укажите следующие свойства в hello **приемник**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-990">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-990">Property</span></span> | <span data-ttu-id="98caf-991">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-991">Description</span></span> | <span data-ttu-id="98caf-992">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-992">Allowed values</span></span> | <span data-ttu-id="98caf-993">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="98caf-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="98caf-994">WriteBehavior</span></span> | <span data-ttu-id="98caf-995">Указывает ли toomerge или замены, если документ уже существует в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="98caf-996">Merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-996">Merge (default)</span></span><br/><span data-ttu-id="98caf-997">Отправить</span><span class="sxs-lookup"><span data-stu-id="98caf-997">Upload</span></span>| <span data-ttu-id="98caf-998">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-998">No</span></span> |
| <span data-ttu-id="98caf-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-999">WriteBatchSize</span></span> | <span data-ttu-id="98caf-1000">Передает данные в индекс поиска Azure hello достижении writeBatchSize hello размер буфера.</span><span class="sxs-lookup"><span data-stu-id="98caf-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="98caf-1001">1 too1 000.</span><span class="sxs-lookup"><span data-stu-id="98caf-1001">1 too1,000.</span></span> <span data-ttu-id="98caf-1002">Значение по умолчанию — 1000.</span><span class="sxs-lookup"><span data-stu-id="98caf-1002">Default value is 1000.</span></span> | <span data-ttu-id="98caf-1003">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1004">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-1005">Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="98caf-1006">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1007">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1007">Linked service</span></span>
<span data-ttu-id="98caf-1008">Существует два типа связанных служб: связанная служба хранилища Azure и связанная служба SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="98caf-1009">Связанная служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="98caf-1010">toolink фабрики данных tooa учетной записи хранилища Azure с помощью hello **ключ учетной записи**, создания связанной службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="98caf-1011">Хранилище Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="98caf-1012">Затем можно указать следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1013">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1013">Property</span></span> | <span data-ttu-id="98caf-1014">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1014">Description</span></span> | <span data-ttu-id="98caf-1015">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-1016">type</span><span class="sxs-lookup"><span data-stu-id="98caf-1016">type</span></span> |<span data-ttu-id="98caf-1017">свойство типа Hello должно быть присвоено: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="98caf-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="98caf-1018">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1018">Yes</span></span> |
| <span data-ttu-id="98caf-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-1019">connectionString</span></span> |<span data-ttu-id="98caf-1020">Укажите сведения, необходимые для свойства connectionString hello tooconnect tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="98caf-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="98caf-1021">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1021">Yes</span></span> |

<span data-ttu-id="98caf-1022">**Пример**</span><span class="sxs-lookup"><span data-stu-id="98caf-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="98caf-1023">Связанная служба SAS хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="98caf-1024">Hello связаны SAS хранилища Azure службы позволяет toolink фабрикой данных Azure tooan учетной записи хранилища Azure с помощью подписи общего доступа (SAS).</span><span class="sxs-lookup"><span data-stu-id="98caf-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="98caf-1025">Он предоставляет hello фабрики данных ограничен или ограниченным временем доступа ресурсов, связанных с/tooall (/ контейнер больших двоичных объектов) в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="98caf-1026">toolink фабрики данных tooa учетной записи хранилища Azure с помощью подписи общего доступа, создания службы связаны SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="98caf-1027">toodefine SAS хранилища Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="98caf-1028">Затем можно указать следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="98caf-1029">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1029">Property</span></span> | <span data-ttu-id="98caf-1030">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1030">Description</span></span> | <span data-ttu-id="98caf-1031">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-1032">type</span><span class="sxs-lookup"><span data-stu-id="98caf-1032">type</span></span> |<span data-ttu-id="98caf-1033">свойство типа Hello должно быть присвоено: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="98caf-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="98caf-1034">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1034">Yes</span></span> |
| <span data-ttu-id="98caf-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="98caf-1035">sasUri</span></span> |<span data-ttu-id="98caf-1036">Укажите общий URI подписи доступа toohello хранилища Azure ресурсы, такие как BLOB-объекта, контейнера или таблицы.</span><span class="sxs-lookup"><span data-stu-id="98caf-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="98caf-1037">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1037">Yes</span></span> |

<span data-ttu-id="98caf-1038">**Пример**</span><span class="sxs-lookup"><span data-stu-id="98caf-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="98caf-1039">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1040">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1040">Dataset</span></span>
<span data-ttu-id="98caf-1041">toodefine набор таблиц Azure hello набор **тип** hello набора данных слишком**AzureTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1042">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1042">Property</span></span> | <span data-ttu-id="98caf-1043">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1043">Description</span></span> | <span data-ttu-id="98caf-1044">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1045">tableName</span></span> |<span data-ttu-id="98caf-1046">Имя таблицы hello в экземпляре базы данных таблицы Azure hello, что связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="98caf-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="98caf-1047">Да.</span><span class="sxs-lookup"><span data-stu-id="98caf-1047">Yes.</span></span> <span data-ttu-id="98caf-1048">При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="98caf-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="98caf-1049">Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="98caf-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1050">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1051">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="98caf-1052">Источник таблицы Azure в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1053">При копировании данных из табличного хранилища Azure, задайте hello **тип источника** из hello в действии копирования слишком**AzureTableSource**и укажите следующие свойства в hello **источника**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1054">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1054">Property</span></span> | <span data-ttu-id="98caf-1055">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1055">Description</span></span> | <span data-ttu-id="98caf-1056">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1056">Allowed values</span></span> | <span data-ttu-id="98caf-1057">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="98caf-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="98caf-1059">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1060">Строка запроса таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-1060">Azure table query string.</span></span> <span data-ttu-id="98caf-1061">Примеры в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1061">See examples in hello next section.</span></span> |<span data-ttu-id="98caf-1062">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-1062">No.</span></span> <span data-ttu-id="98caf-1063">При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="98caf-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="98caf-1064">Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения.</span><span class="sxs-lookup"><span data-stu-id="98caf-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="98caf-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="98caf-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="98caf-1066">Указывают ли проглотить исключение hello таблицы не существует.</span><span class="sxs-lookup"><span data-stu-id="98caf-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="98caf-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="98caf-1067">TRUE</span></span><br/><span data-ttu-id="98caf-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="98caf-1068">FALSE</span></span> |<span data-ttu-id="98caf-1069">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1070">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-1071">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="98caf-1072">Приемник таблицы Azure в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-1073">При копировании данных tooAzure хранилище таблиц задать hello **тип приемника** из hello в действии копирования слишком**AzureTableSink**и укажите следующие свойства в hello **приемник** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-1074">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1074">Property</span></span> | <span data-ttu-id="98caf-1075">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1075">Description</span></span> | <span data-ttu-id="98caf-1076">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1076">Allowed values</span></span> | <span data-ttu-id="98caf-1077">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="98caf-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="98caf-1079">Значение по умолчанию раздел ключа, может использоваться приемником hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="98caf-1080">Строковое значение.</span><span class="sxs-lookup"><span data-stu-id="98caf-1080">A string value.</span></span> |<span data-ttu-id="98caf-1081">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1081">No</span></span> |
| <span data-ttu-id="98caf-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="98caf-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="98caf-1083">Укажите имя столбца hello, значения которых используются в качестве ключей секционирования.</span><span class="sxs-lookup"><span data-stu-id="98caf-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="98caf-1084">Если не указано, в качестве ключа секции hello используется AzureTableDefaultPartitionKeyValue.</span><span class="sxs-lookup"><span data-stu-id="98caf-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="98caf-1085">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="98caf-1085">A column name.</span></span> |<span data-ttu-id="98caf-1086">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1086">No</span></span> |
| <span data-ttu-id="98caf-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="98caf-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="98caf-1088">Укажите имя столбца hello, значение которого используются в качестве ключа строки.</span><span class="sxs-lookup"><span data-stu-id="98caf-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="98caf-1089">Если имя не указано, используйте для каждой строки идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="98caf-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="98caf-1090">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="98caf-1090">A column name.</span></span> |<span data-ttu-id="98caf-1091">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1091">No</span></span> |
| <span data-ttu-id="98caf-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="98caf-1092">azureTableInsertType</span></span> |<span data-ttu-id="98caf-1093">режим Hello tooinsert данные в таблицу Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="98caf-1094">Это свойство определяет, имеют ли существующие строки в выходной диапазон hello соответствующие ключи секций и строк значениями заменить или слияние.</span><span class="sxs-lookup"><span data-stu-id="98caf-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="98caf-1095">toolearn о работе этих параметров (слияния и замены) в разделе [Вставка или слияние сущности](https://msdn.microsoft.com/library/azure/hh452241.aspx) и [Вставка или замена сущности](https://msdn.microsoft.com/library/azure/hh452242.aspx) разделы.</span><span class="sxs-lookup"><span data-stu-id="98caf-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="98caf-1096">Этот параметр применяется на уровне строк hello, не уровне hello таблицы и ни один из параметров удаляются строки в таблице вывода hello, которые не существуют во входном файле hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="98caf-1097">merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-1097">merge (default)</span></span><br/><span data-ttu-id="98caf-1098">replace</span><span class="sxs-lookup"><span data-stu-id="98caf-1098">replace</span></span> |<span data-ttu-id="98caf-1099">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1099">No</span></span> |
| <span data-ttu-id="98caf-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-1100">writeBatchSize</span></span> |<span data-ttu-id="98caf-1101">Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="98caf-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="98caf-1102">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="98caf-1102">Integer (number of rows)</span></span> |<span data-ttu-id="98caf-1103">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="98caf-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="98caf-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-1104">writeBatchTimeout</span></span> |<span data-ttu-id="98caf-1105">Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="98caf-1106">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="98caf-1106">timespan</span></span><br/><br/><span data-ttu-id="98caf-1107">Пример: 00:20:00 (20 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="98caf-1108">Нет (время ожидания по умолчанию клиент toostorage по умолчанию значение составляет 90 сек)</span><span class="sxs-lookup"><span data-stu-id="98caf-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1109">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="98caf-1110">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="98caf-1111">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="98caf-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1112">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1112">Linked service</span></span>
<span data-ttu-id="98caf-1113">toodefine Amazon Redshift связанной службы, набор hello **тип** hello связанной службы слишком**AmazonRedshift**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1114">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1114">Property</span></span> | <span data-ttu-id="98caf-1115">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1115">Description</span></span> | <span data-ttu-id="98caf-1116">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1117">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1117">server</span></span> |<span data-ttu-id="98caf-1118">IP-адрес или имя сервера Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="98caf-1119">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1119">Yes</span></span> |
| <span data-ttu-id="98caf-1120">порт</span><span class="sxs-lookup"><span data-stu-id="98caf-1120">port</span></span> |<span data-ttu-id="98caf-1121">Hello номер порта TCP hello hello Amazon Redshift сервер использует toolisten для клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="98caf-1122">Нет, значение по умолчанию — 5439.</span><span class="sxs-lookup"><span data-stu-id="98caf-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="98caf-1123">database</span><span class="sxs-lookup"><span data-stu-id="98caf-1123">database</span></span> |<span data-ttu-id="98caf-1124">Имя базы данных Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="98caf-1125">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1125">Yes</span></span> |
| <span data-ttu-id="98caf-1126">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1126">username</span></span> |<span data-ttu-id="98caf-1127">Имя пользователя, имеющего доступ к базе данных toohello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="98caf-1128">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1128">Yes</span></span> |
| <span data-ttu-id="98caf-1129">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1129">password</span></span> |<span data-ttu-id="98caf-1130">Пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1130">Password for hello user account.</span></span> |<span data-ttu-id="98caf-1131">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1132">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="98caf-1133">Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1134">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1134">Dataset</span></span>
<span data-ttu-id="98caf-1135">toodefine набору данных Amazon Redshift hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1136">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1136">Property</span></span> | <span data-ttu-id="98caf-1137">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1137">Description</span></span> | <span data-ttu-id="98caf-1138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1139">tableName</span></span> |<span data-ttu-id="98caf-1140">Имя таблицы hello в базе данных Amazon Redshift hello, связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="98caf-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="98caf-1141">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="98caf-1142">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="98caf-1143">Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1144">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="98caf-1145">При копировании данных из Amazon Redshift задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1146">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1146">Property</span></span> | <span data-ttu-id="98caf-1147">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1147">Description</span></span> | <span data-ttu-id="98caf-1148">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1148">Allowed values</span></span> | <span data-ttu-id="98caf-1149">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1150">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1150">query</span></span> |<span data-ttu-id="98caf-1151">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1152">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1152">SQL query string.</span></span> <span data-ttu-id="98caf-1153">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-1154">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1155">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="98caf-1156">Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="98caf-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="98caf-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1158">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1158">Linked service</span></span>
<span data-ttu-id="98caf-1159">toodefine IBM DB2 связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesDB2**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1160">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1160">Property</span></span> | <span data-ttu-id="98caf-1161">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1161">Description</span></span> | <span data-ttu-id="98caf-1162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1163">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1163">server</span></span> |<span data-ttu-id="98caf-1164">Имя сервера hello DB2.</span><span class="sxs-lookup"><span data-stu-id="98caf-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="98caf-1165">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1165">Yes</span></span> |
| <span data-ttu-id="98caf-1166">database</span><span class="sxs-lookup"><span data-stu-id="98caf-1166">database</span></span> |<span data-ttu-id="98caf-1167">Имя базы данных hello DB2.</span><span class="sxs-lookup"><span data-stu-id="98caf-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="98caf-1168">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1168">Yes</span></span> |
| <span data-ttu-id="98caf-1169">schema</span><span class="sxs-lookup"><span data-stu-id="98caf-1169">schema</span></span> |<span data-ttu-id="98caf-1170">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="98caf-1171">Имя схемы Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="98caf-1172">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1172">No</span></span> |
| <span data-ttu-id="98caf-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1173">authenticationType</span></span> |<span data-ttu-id="98caf-1174">Тип проверки подлинности используется база данных DB2 toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="98caf-1175">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="98caf-1176">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1176">Yes</span></span> |
| <span data-ttu-id="98caf-1177">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1177">username</span></span> |<span data-ttu-id="98caf-1178">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="98caf-1179">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1179">No</span></span> |
| <span data-ttu-id="98caf-1180">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1180">password</span></span> |<span data-ttu-id="98caf-1181">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-1182">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1182">No</span></span> |
| <span data-ttu-id="98caf-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1183">gatewayName</span></span> |<span data-ttu-id="98caf-1184">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных DB2.</span><span class="sxs-lookup"><span data-stu-id="98caf-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="98caf-1185">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1186">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="98caf-1187">Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1188">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1188">Dataset</span></span>
<span data-ttu-id="98caf-1189">набор данных toodefine DB2, набор hello **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="98caf-1190">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1190">Property</span></span> | <span data-ttu-id="98caf-1191">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1191">Description</span></span> | <span data-ttu-id="98caf-1192">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1193">tableName</span></span> |<span data-ttu-id="98caf-1194">Имя таблицы hello в экземпляре базы данных DB2 hello, что связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="98caf-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="98caf-1195">Hello tableName учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="98caf-1196">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="98caf-1197">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1198">Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1199">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1200">При копировании данных из IBM DB2, задайте hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1201">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1201">Property</span></span> | <span data-ttu-id="98caf-1202">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1202">Description</span></span> | <span data-ttu-id="98caf-1203">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1203">Allowed values</span></span> | <span data-ttu-id="98caf-1204">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1205">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1205">query</span></span> |<span data-ttu-id="98caf-1206">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1207">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1207">SQL query string.</span></span> <span data-ttu-id="98caf-1208">Например, `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="98caf-1209">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1210">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="98caf-1211">Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="98caf-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="98caf-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1213">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1213">Linked service</span></span>
<span data-ttu-id="98caf-1214">toodefine MySQL связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesMySql**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1215">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1215">Property</span></span> | <span data-ttu-id="98caf-1216">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1216">Description</span></span> | <span data-ttu-id="98caf-1217">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1218">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1218">server</span></span> |<span data-ttu-id="98caf-1219">Имя сервера MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="98caf-1220">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1220">Yes</span></span> |
| <span data-ttu-id="98caf-1221">database</span><span class="sxs-lookup"><span data-stu-id="98caf-1221">database</span></span> |<span data-ttu-id="98caf-1222">Имя базы данных MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="98caf-1223">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1223">Yes</span></span> |
| <span data-ttu-id="98caf-1224">schema</span><span class="sxs-lookup"><span data-stu-id="98caf-1224">schema</span></span> |<span data-ttu-id="98caf-1225">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="98caf-1226">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1226">No</span></span> |
| <span data-ttu-id="98caf-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1227">authenticationType</span></span> |<span data-ttu-id="98caf-1228">Тип проверки подлинности используется база данных MySQL toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="98caf-1229">Возможные значения: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="98caf-1230">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1230">Yes</span></span> |
| <span data-ttu-id="98caf-1231">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1231">username</span></span> |<span data-ttu-id="98caf-1232">Укажите базу данных MySQL toohello tooconnect имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="98caf-1233">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1233">Yes</span></span> |
| <span data-ttu-id="98caf-1234">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1234">password</span></span> |<span data-ttu-id="98caf-1235">Укажите пароль для учетной записи пользователя hello указанное.</span><span class="sxs-lookup"><span data-stu-id="98caf-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="98caf-1236">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1236">Yes</span></span> |
| <span data-ttu-id="98caf-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1237">gatewayName</span></span> |<span data-ttu-id="98caf-1238">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="98caf-1239">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1240">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="98caf-1241">Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1242">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1242">Dataset</span></span>
<span data-ttu-id="98caf-1243">toodefine набора данных MySQL, набор hello **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1244">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1244">Property</span></span> | <span data-ttu-id="98caf-1245">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1245">Description</span></span> | <span data-ttu-id="98caf-1246">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1247">tableName</span></span> |<span data-ttu-id="98caf-1248">Имя таблицы hello в экземпляр базы данных MySQL, который ссылается связанная служба hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="98caf-1249">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1250">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="98caf-1251">Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1252">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1253">При копировании данных из базы данных MySQL, задайте hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1254">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1254">Property</span></span> | <span data-ttu-id="98caf-1255">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1255">Description</span></span> | <span data-ttu-id="98caf-1256">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1256">Allowed values</span></span> | <span data-ttu-id="98caf-1257">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1258">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1258">query</span></span> |<span data-ttu-id="98caf-1259">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1260">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1260">SQL query string.</span></span> <span data-ttu-id="98caf-1261">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-1262">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="98caf-1263">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1264">Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="98caf-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="98caf-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-1266">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1266">Linked service</span></span>
<span data-ttu-id="98caf-1267">toodefine Oracle связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesOracle**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1268">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1268">Property</span></span> | <span data-ttu-id="98caf-1269">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1269">Description</span></span> | <span data-ttu-id="98caf-1270">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="98caf-1271">driverType</span></span> | <span data-ttu-id="98caf-1272">Указать, какие данные toocopy драйвер toouse из / tooOracle базы данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="98caf-1273">Допустимые значения: **Майкрософт** или **ODP** (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="98caf-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="98caf-1274">Дополнительные сведения о драйверах см. в разделе [Поддерживаемые версии и установка](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="98caf-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="98caf-1275">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1275">No</span></span> |
| <span data-ttu-id="98caf-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-1276">connectionString</span></span> | <span data-ttu-id="98caf-1277">Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных Oracle toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="98caf-1278">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1278">Yes</span></span> |
| <span data-ttu-id="98caf-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1279">gatewayName</span></span> | <span data-ttu-id="98caf-1280">Имя шлюза hello, что является toohello tooconnect используется локальный сервер Oracle</span><span class="sxs-lookup"><span data-stu-id="98caf-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="98caf-1281">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1282">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="98caf-1283">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1284">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1284">Dataset</span></span>
<span data-ttu-id="98caf-1285">toodefine набору данных Oracle hello набор **тип** hello набора данных слишком**OracleTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1286">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1286">Property</span></span> | <span data-ttu-id="98caf-1287">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1287">Description</span></span> | <span data-ttu-id="98caf-1288">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1289">tableName</span></span> |<span data-ttu-id="98caf-1290">Имя таблицы hello в hello базы данных Oracle, hello связанной службы относится.</span><span class="sxs-lookup"><span data-stu-id="98caf-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="98caf-1291">Нет (если указан параметр **oracleReaderQuery** объекта **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="98caf-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1292">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="98caf-1293">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="98caf-1294">Источник Oracle в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1295">При копировании данных из базы данных Oracle, задайте hello **тип источника** из hello в действии копирования слишком**OracleSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1296">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1296">Property</span></span> | <span data-ttu-id="98caf-1297">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1297">Description</span></span> | <span data-ttu-id="98caf-1298">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1298">Allowed values</span></span> | <span data-ttu-id="98caf-1299">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="98caf-1300">oracleReaderQuery</span></span> |<span data-ttu-id="98caf-1301">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1302">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1302">SQL query string.</span></span> <span data-ttu-id="98caf-1303">Например: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="98caf-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="98caf-1304">Если не указан, hello выполняемой инструкции SQL:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="98caf-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="98caf-1305">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1306">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-1307">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="98caf-1308">Приемник Oracle в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-1309">При копировании базы данных Oracle tooam данных задайте hello **тип приемника** из hello в действии копирования слишком**OracleSink**и укажите следующие свойства в hello **приемник** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-1310">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1310">Property</span></span> | <span data-ttu-id="98caf-1311">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1311">Description</span></span> | <span data-ttu-id="98caf-1312">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1312">Allowed values</span></span> | <span data-ttu-id="98caf-1313">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-1314">writeBatchTimeout</span></span> |<span data-ttu-id="98caf-1315">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="98caf-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="98caf-1316">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="98caf-1316">timespan</span></span><br/><br/> <span data-ttu-id="98caf-1317">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="98caf-1318">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1318">No</span></span> |
| <span data-ttu-id="98caf-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-1319">writeBatchSize</span></span> |<span data-ttu-id="98caf-1320">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="98caf-1321">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="98caf-1321">Integer (number of rows)</span></span> |<span data-ttu-id="98caf-1322">Нет (значение по умолчанию — 100)</span><span class="sxs-lookup"><span data-stu-id="98caf-1322">No (default: 100)</span></span> |
| <span data-ttu-id="98caf-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="98caf-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="98caf-1324">Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="98caf-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="98caf-1325">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1325">A query statement.</span></span> |<span data-ttu-id="98caf-1326">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1326">No</span></span> |
| <span data-ttu-id="98caf-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="98caf-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="98caf-1328">Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="98caf-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="98caf-1329">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="98caf-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="98caf-1330">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1331">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="98caf-1332">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="98caf-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="98caf-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1334">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1334">Linked service</span></span>
<span data-ttu-id="98caf-1335">toodefine PostgreSQL связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesPostgreSql**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1336">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1336">Property</span></span> | <span data-ttu-id="98caf-1337">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1337">Description</span></span> | <span data-ttu-id="98caf-1338">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1339">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1339">server</span></span> |<span data-ttu-id="98caf-1340">Имя сервера PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="98caf-1341">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1341">Yes</span></span> |
| <span data-ttu-id="98caf-1342">database</span><span class="sxs-lookup"><span data-stu-id="98caf-1342">database</span></span> |<span data-ttu-id="98caf-1343">Имя базы данных PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="98caf-1344">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1344">Yes</span></span> |
| <span data-ttu-id="98caf-1345">schema</span><span class="sxs-lookup"><span data-stu-id="98caf-1345">schema</span></span> |<span data-ttu-id="98caf-1346">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="98caf-1347">Имя схемы Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="98caf-1348">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1348">No</span></span> |
| <span data-ttu-id="98caf-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1349">authenticationType</span></span> |<span data-ttu-id="98caf-1350">Тип проверки подлинности используется база данных PostgreSQL toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="98caf-1351">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="98caf-1352">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1352">Yes</span></span> |
| <span data-ttu-id="98caf-1353">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1353">username</span></span> |<span data-ttu-id="98caf-1354">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="98caf-1355">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1355">No</span></span> |
| <span data-ttu-id="98caf-1356">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1356">password</span></span> |<span data-ttu-id="98caf-1357">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-1358">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1358">No</span></span> |
| <span data-ttu-id="98caf-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1359">gatewayName</span></span> |<span data-ttu-id="98caf-1360">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальная база данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="98caf-1361">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1362">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="98caf-1363">Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1364">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1364">Dataset</span></span>
<span data-ttu-id="98caf-1365">toodefine набора данных PostgreSQL hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1366">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1366">Property</span></span> | <span data-ttu-id="98caf-1367">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1367">Description</span></span> | <span data-ttu-id="98caf-1368">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1369">tableName</span></span> |<span data-ttu-id="98caf-1370">Имя таблицы hello в экземпляр базы данных PostgreSQL, который ссылается связанная служба hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="98caf-1371">Hello tableName учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="98caf-1372">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1373">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="98caf-1374">Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1375">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1376">При копировании данных из базы данных PostgreSQL задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1377">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1377">Property</span></span> | <span data-ttu-id="98caf-1378">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1378">Description</span></span> | <span data-ttu-id="98caf-1379">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1379">Allowed values</span></span> | <span data-ttu-id="98caf-1380">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1381">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1381">query</span></span> |<span data-ttu-id="98caf-1382">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1383">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1383">SQL query string.</span></span> <span data-ttu-id="98caf-1384">Например, "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="98caf-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="98caf-1385">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1386">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1387">Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="98caf-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="98caf-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-1389">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1389">Linked service</span></span>
<span data-ttu-id="98caf-1390">toodefine хранилища SAP Business (BW) связанной службы, набор hello **тип** hello связанной службы слишком**SapBw**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="98caf-1391">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1391">Property</span></span> | <span data-ttu-id="98caf-1392">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1392">Description</span></span> | <span data-ttu-id="98caf-1393">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1393">Allowed values</span></span> | <span data-ttu-id="98caf-1394">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="98caf-1395">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1395">server</span></span> | <span data-ttu-id="98caf-1396">Имя сервера hello, на какие hello SAP BW расположен экземпляр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="98caf-1397">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1397">string</span></span> | <span data-ttu-id="98caf-1398">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1398">Yes</span></span>
<span data-ttu-id="98caf-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="98caf-1399">systemNumber</span></span> | <span data-ttu-id="98caf-1400">Номер системы hello системы SAP BW.</span><span class="sxs-lookup"><span data-stu-id="98caf-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="98caf-1401">Двузначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="98caf-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="98caf-1402">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1402">Yes</span></span>
<span data-ttu-id="98caf-1403">clientid</span><span class="sxs-lookup"><span data-stu-id="98caf-1403">clientId</span></span> | <span data-ttu-id="98caf-1404">Идентификатор клиента для клиента hello в hello системы SAP-W.</span><span class="sxs-lookup"><span data-stu-id="98caf-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="98caf-1405">Трехзначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="98caf-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="98caf-1406">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1406">Yes</span></span>
<span data-ttu-id="98caf-1407">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1407">username</span></span> | <span data-ttu-id="98caf-1408">Имя пользователя hello с сервера SAP toohello доступа</span><span class="sxs-lookup"><span data-stu-id="98caf-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="98caf-1409">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1409">string</span></span> | <span data-ttu-id="98caf-1410">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1410">Yes</span></span>
<span data-ttu-id="98caf-1411">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1411">password</span></span> | <span data-ttu-id="98caf-1412">Пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1412">Password for hello user.</span></span> | <span data-ttu-id="98caf-1413">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1413">string</span></span> | <span data-ttu-id="98caf-1414">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1414">Yes</span></span>
<span data-ttu-id="98caf-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1415">gatewayName</span></span> | <span data-ttu-id="98caf-1416">Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP BW экземпляр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="98caf-1417">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1417">string</span></span> | <span data-ttu-id="98caf-1418">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1418">Yes</span></span>
<span data-ttu-id="98caf-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-1419">encryptedCredential</span></span> | <span data-ttu-id="98caf-1420">Строка Hello шифрования учетных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="98caf-1421">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1421">string</span></span> | <span data-ttu-id="98caf-1422">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-1423">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="98caf-1424">Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1425">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1425">Dataset</span></span>
<span data-ttu-id="98caf-1426">toodefine набора данных SAP BW hello набор **тип** hello набора данных слишком**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="98caf-1427">Свойства определенного типа, не поддерживается для набора данных SAP BW hello типа **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="98caf-1428">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="98caf-1429">Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1430">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1431">При копировании данных из SAP Business Warehouse задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1432">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1432">Property</span></span> | <span data-ttu-id="98caf-1433">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1433">Description</span></span> | <span data-ttu-id="98caf-1434">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1434">Allowed values</span></span> | <span data-ttu-id="98caf-1435">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1436">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1436">query</span></span> | <span data-ttu-id="98caf-1437">Указывает tooread hello многомерных Выражений запроса данных из экземпляра SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="98caf-1438">Запрос многомерных выражений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1438">MDX query.</span></span> | <span data-ttu-id="98caf-1439">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1440">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1441">Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="98caf-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="98caf-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1443">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1443">Linked service</span></span>
<span data-ttu-id="98caf-1444">SAP HANA toodefine связанной службы, набор hello **тип** hello связанной службы слишком**SapHana**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="98caf-1445">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1445">Property</span></span> | <span data-ttu-id="98caf-1446">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1446">Description</span></span> | <span data-ttu-id="98caf-1447">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1447">Allowed values</span></span> | <span data-ttu-id="98caf-1448">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="98caf-1449">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1449">server</span></span> | <span data-ttu-id="98caf-1450">Имя сервера hello, на какие hello SAP HANA расположен экземпляр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="98caf-1451">Если ваш сервер использует настроенный порт, укажите `server:port`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="98caf-1452">строка</span><span class="sxs-lookup"><span data-stu-id="98caf-1452">string</span></span> | <span data-ttu-id="98caf-1453">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1453">Yes</span></span>
<span data-ttu-id="98caf-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1454">authenticationType</span></span> | <span data-ttu-id="98caf-1455">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="98caf-1455">Type of authentication.</span></span> | <span data-ttu-id="98caf-1456">string.</span><span class="sxs-lookup"><span data-stu-id="98caf-1456">string.</span></span> <span data-ttu-id="98caf-1457">Basic или Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="98caf-1458">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1458">Yes</span></span> 
<span data-ttu-id="98caf-1459">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1459">username</span></span> | <span data-ttu-id="98caf-1460">Имя пользователя hello с сервера SAP toohello доступа</span><span class="sxs-lookup"><span data-stu-id="98caf-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="98caf-1461">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1461">string</span></span> | <span data-ttu-id="98caf-1462">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1462">Yes</span></span>
<span data-ttu-id="98caf-1463">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1463">password</span></span> | <span data-ttu-id="98caf-1464">Пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1464">Password for hello user.</span></span> | <span data-ttu-id="98caf-1465">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1465">string</span></span> | <span data-ttu-id="98caf-1466">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1466">Yes</span></span>
<span data-ttu-id="98caf-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1467">gatewayName</span></span> | <span data-ttu-id="98caf-1468">Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP HANA экземпляр.</span><span class="sxs-lookup"><span data-stu-id="98caf-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="98caf-1469">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1469">string</span></span> | <span data-ttu-id="98caf-1470">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1470">Yes</span></span>
<span data-ttu-id="98caf-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-1471">encryptedCredential</span></span> | <span data-ttu-id="98caf-1472">Строка Hello шифрования учетных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="98caf-1473">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1473">string</span></span> | <span data-ttu-id="98caf-1474">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-1475">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="98caf-1476">Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="98caf-1477">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1477">Dataset</span></span>
<span data-ttu-id="98caf-1478">toodefine набора данных SAP HANA hello набор **тип** hello набора данных слишком**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="98caf-1479">Свойства конкретного типа, не поддерживается для набора данных SAP HANA hello типа **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="98caf-1480">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="98caf-1481">Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1482">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1483">При копировании данных из хранилища данных SAP HANA задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1484">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1484">Property</span></span> | <span data-ttu-id="98caf-1485">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1485">Description</span></span> | <span data-ttu-id="98caf-1486">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1486">Allowed values</span></span> | <span data-ttu-id="98caf-1487">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1488">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1488">query</span></span> | <span data-ttu-id="98caf-1489">Указывает tooread hello SQL запроса данных из экземпляра SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="98caf-1490">SQL-запрос.</span><span class="sxs-lookup"><span data-stu-id="98caf-1490">SQL query.</span></span> | <span data-ttu-id="98caf-1491">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="98caf-1492">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1493">Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="98caf-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="98caf-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1495">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1495">Linked service</span></span>
<span data-ttu-id="98caf-1496">Создание связанной службы типа **OnPremisesSqlServer** toolink фабрикой данных базы данных tooa в локальной среде SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="98caf-1497">Привет, в следующей таблице приводится описание JSON элементов определенного tooon локальной связанной службы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="98caf-1498">Привет, в следующей таблице приводится описание tooSQL определенные элементы JSON службы связанного сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="98caf-1499">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1499">Property</span></span> | <span data-ttu-id="98caf-1500">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1500">Description</span></span> | <span data-ttu-id="98caf-1501">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1502">type</span><span class="sxs-lookup"><span data-stu-id="98caf-1502">type</span></span> |<span data-ttu-id="98caf-1503">свойство типа Hello должно быть присвоено: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="98caf-1504">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1504">Yes</span></span> |
| <span data-ttu-id="98caf-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-1505">connectionString</span></span> |<span data-ttu-id="98caf-1506">Укажите сведения connectionString, необходимые tooconnect toohello локальной SQL Server базы данных с помощью проверки подлинности Windows или проверка подлинности SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="98caf-1507">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1507">Yes</span></span> |
| <span data-ttu-id="98caf-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1508">gatewayName</span></span> |<span data-ttu-id="98caf-1509">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="98caf-1510">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1510">Yes</span></span> |
| <span data-ttu-id="98caf-1511">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1511">username</span></span> |<span data-ttu-id="98caf-1512">При использовании проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="98caf-1513">Например, **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="98caf-1514">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1514">No</span></span> |
| <span data-ttu-id="98caf-1515">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1515">password</span></span> |<span data-ttu-id="98caf-1516">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-1517">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1517">No</span></span> |

<span data-ttu-id="98caf-1518">Вы можете зашифровать учетные данные с помощью hello **New AzureRmDataFactoryEncryptValue** командлета и использовать их в строке подключения hello, как показано в следующий пример hello (**EncryptedCredential** свойство):</span><span class="sxs-lookup"><span data-stu-id="98caf-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="98caf-1519">Пример: JSON для использования проверки подлинности SQL</span><span class="sxs-lookup"><span data-stu-id="98caf-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="98caf-1520">Пример: JSON для использования проверки подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="98caf-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="98caf-1521">Если указаны имя пользователя и пароль, шлюз использует их tooimpersonate hello базы данных SQL Server в локальной toohello в tooconnect учетную запись указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="98caf-1522">В противном случае шлюз подключается toohello SQL Server непосредственно с контекстом безопасности hello шлюза (его учетная запись для запуска).</span><span class="sxs-lookup"><span data-stu-id="98caf-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="98caf-1523">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1524">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1524">Dataset</span></span>
<span data-ttu-id="98caf-1525">toodefine набора данных SQL Server, набор hello **тип** hello набора данных слишком**SqlServerTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1526">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1526">Property</span></span> | <span data-ttu-id="98caf-1527">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1527">Description</span></span> | <span data-ttu-id="98caf-1528">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1529">tableName</span></span> |<span data-ttu-id="98caf-1530">Имя hello таблицы или представления в экземпляр базы данных SQL Server hello, связанная служба ссылается.</span><span class="sxs-lookup"><span data-stu-id="98caf-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="98caf-1531">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1532">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1533">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="98caf-1534">Источник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1535">При копировании данных из базы данных SQL Server, задайте hello **тип источника** из hello в действии копирования слишком**SqlSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1536">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1536">Property</span></span> | <span data-ttu-id="98caf-1537">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1537">Description</span></span> | <span data-ttu-id="98caf-1538">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1538">Allowed values</span></span> | <span data-ttu-id="98caf-1539">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="98caf-1540">sqlReaderQuery</span></span> |<span data-ttu-id="98caf-1541">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1542">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1542">SQL query string.</span></span> <span data-ttu-id="98caf-1543">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="98caf-1544">Может ссылаться на несколько таблиц из базы данных hello ссылается hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="98caf-1545">Если не указан, hello выполняемой инструкции SQL: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="98caf-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="98caf-1546">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1546">No</span></span> |
| <span data-ttu-id="98caf-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="98caf-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="98caf-1548">Имя hello хранимой процедуры, который считывает данные из таблицы источника hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="98caf-1549">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="98caf-1550">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1550">No</span></span> |
| <span data-ttu-id="98caf-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-1551">storedProcedureParameters</span></span> |<span data-ttu-id="98caf-1552">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="98caf-1553">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1553">Name/value pairs.</span></span> <span data-ttu-id="98caf-1554">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="98caf-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="98caf-1555">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1555">No</span></span> |

<span data-ttu-id="98caf-1556">Если hello **sqlReaderQuery** указан для hello SqlSource, hello действие копирования выполняет этот запрос данных hello базы данных SQL Server источника tooget hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="98caf-1557">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="98caf-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="98caf-1558">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используемые toobuild toorun запрос select для hello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="98caf-1559">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="98caf-1560">При использовании **sqlReaderStoredProcedureName**, по-прежнему требуется toospecify значение для hello **tableName** свойство в наборе данных hello JSON.</span><span class="sxs-lookup"><span data-stu-id="98caf-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="98caf-1561">Хотя какие-либо проверки этой таблицы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="98caf-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="98caf-1562">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-1563">В этом примере **sqlReaderQuery** указан для hello SqlSource.</span><span class="sxs-lookup"><span data-stu-id="98caf-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="98caf-1564">Действие копирования Hello этот запрос запускает hello tooget hello базы данных SQL Server исходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="98caf-1565">Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="98caf-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="98caf-1566">Hello sqlReaderQuery ссылаться на несколько таблиц в базе данных hello ссылается hello входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="98caf-1567">Это не таблица hello ограниченный tooonly, задайте как hello typeProperty tableName набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="98caf-1568">Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используется toobuild toorun запрос select для hello базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="98caf-1569">Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="98caf-1570">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="98caf-1571">Приемник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-1572">При копировании базы данных SQL Server tooa данных задайте hello **тип приемника** из hello в действии копирования слишком**SqlSink**и укажите следующие свойства в hello **приемник** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-1573">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1573">Property</span></span> | <span data-ttu-id="98caf-1574">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1574">Description</span></span> | <span data-ttu-id="98caf-1575">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1575">Allowed values</span></span> | <span data-ttu-id="98caf-1576">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-1577">writeBatchTimeout</span></span> |<span data-ttu-id="98caf-1578">Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="98caf-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="98caf-1579">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="98caf-1579">timespan</span></span><br/><br/> <span data-ttu-id="98caf-1580">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="98caf-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="98caf-1581">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1581">No</span></span> |
| <span data-ttu-id="98caf-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="98caf-1582">writeBatchSize</span></span> |<span data-ttu-id="98caf-1583">Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="98caf-1584">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="98caf-1584">Integer (number of rows)</span></span> |<span data-ttu-id="98caf-1585">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="98caf-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="98caf-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="98caf-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="98caf-1587">Укажите запрос для действия копирования tooexecute, таким образом, чтобы очистить данные особый срез.</span><span class="sxs-lookup"><span data-stu-id="98caf-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="98caf-1588">Дополнительные сведения см. в разделе о [повторяемости](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="98caf-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="98caf-1589">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1589">A query statement.</span></span> |<span data-ttu-id="98caf-1590">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1590">No</span></span> |
| <span data-ttu-id="98caf-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="98caf-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="98caf-1592">Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="98caf-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="98caf-1593">Дополнительные сведения см. в разделе о [повторяемости](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="98caf-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="98caf-1594">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="98caf-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="98caf-1595">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1595">No</span></span> |
| <span data-ttu-id="98caf-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="98caf-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="98caf-1597">Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="98caf-1598">Имя hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="98caf-1599">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1599">No</span></span> |
| <span data-ttu-id="98caf-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-1600">storedProcedureParameters</span></span> |<span data-ttu-id="98caf-1601">Параметры для hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="98caf-1602">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1602">Name/value pairs.</span></span> <span data-ttu-id="98caf-1603">Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="98caf-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="98caf-1604">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1604">No</span></span> |
| <span data-ttu-id="98caf-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="98caf-1605">sqlWriterTableType</span></span> |<span data-ttu-id="98caf-1606">Укажите toobe имя типа таблицы, используемых в hello хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="98caf-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="98caf-1607">Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей.</span><span class="sxs-lookup"><span data-stu-id="98caf-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="98caf-1608">Кода хранимой процедуры можно объединять hello данные копируются с существующими данными.</span><span class="sxs-lookup"><span data-stu-id="98caf-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="98caf-1609">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="98caf-1609">A table type name.</span></span> |<span data-ttu-id="98caf-1610">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1611">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1611">Example</span></span>
<span data-ttu-id="98caf-1612">конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час.</span><span class="sxs-lookup"><span data-stu-id="98caf-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="98caf-1613">В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-1614">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="98caf-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="98caf-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1616">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1616">Linked service</span></span>
<span data-ttu-id="98caf-1617">toodefine Sybase связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesSybase**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1618">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1618">Property</span></span> | <span data-ttu-id="98caf-1619">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1619">Description</span></span> | <span data-ttu-id="98caf-1620">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1621">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1621">server</span></span> |<span data-ttu-id="98caf-1622">Имя сервера Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="98caf-1623">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1623">Yes</span></span> |
| <span data-ttu-id="98caf-1624">database</span><span class="sxs-lookup"><span data-stu-id="98caf-1624">database</span></span> |<span data-ttu-id="98caf-1625">Имя базы данных Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="98caf-1626">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1626">Yes</span></span> |
| <span data-ttu-id="98caf-1627">schema</span><span class="sxs-lookup"><span data-stu-id="98caf-1627">schema</span></span> |<span data-ttu-id="98caf-1628">Имя схемы hello в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="98caf-1629">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1629">No</span></span> |
| <span data-ttu-id="98caf-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1630">authenticationType</span></span> |<span data-ttu-id="98caf-1631">Тип проверки подлинности используется база данных Sybase toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="98caf-1632">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="98caf-1633">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1633">Yes</span></span> |
| <span data-ttu-id="98caf-1634">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1634">username</span></span> |<span data-ttu-id="98caf-1635">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="98caf-1636">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1636">No</span></span> |
| <span data-ttu-id="98caf-1637">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1637">password</span></span> |<span data-ttu-id="98caf-1638">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-1639">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1639">No</span></span> |
| <span data-ttu-id="98caf-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1640">gatewayName</span></span> |<span data-ttu-id="98caf-1641">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных Sybase.</span><span class="sxs-lookup"><span data-stu-id="98caf-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="98caf-1642">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1643">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="98caf-1644">Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1645">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1645">Dataset</span></span>
<span data-ttu-id="98caf-1646">toodefine набора данных Sybase hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1647">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1647">Property</span></span> | <span data-ttu-id="98caf-1648">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1648">Description</span></span> | <span data-ttu-id="98caf-1649">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1650">tableName</span></span> |<span data-ttu-id="98caf-1651">Имя таблицы hello в экземпляр базы данных Sybase, который ссылается связанная служба hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="98caf-1652">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1653">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1654">Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1655">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1656">При копировании данных из базы данных Sybase задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1657">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1657">Property</span></span> | <span data-ttu-id="98caf-1658">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1658">Description</span></span> | <span data-ttu-id="98caf-1659">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1659">Allowed values</span></span> | <span data-ttu-id="98caf-1660">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1661">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1661">query</span></span> |<span data-ttu-id="98caf-1662">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1663">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1663">SQL query string.</span></span> <span data-ttu-id="98caf-1664">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-1665">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1666">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1667">Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="98caf-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="98caf-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1669">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1669">Linked service</span></span>
<span data-ttu-id="98caf-1670">toodefine Teradata связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesTeradata**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1671">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1671">Property</span></span> | <span data-ttu-id="98caf-1672">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1672">Description</span></span> | <span data-ttu-id="98caf-1673">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1674">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1674">server</span></span> |<span data-ttu-id="98caf-1675">Имя сервера Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="98caf-1676">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1676">Yes</span></span> |
| <span data-ttu-id="98caf-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1677">authenticationType</span></span> |<span data-ttu-id="98caf-1678">Тип проверки подлинности используется база данных Teradata toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="98caf-1679">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="98caf-1680">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1680">Yes</span></span> |
| <span data-ttu-id="98caf-1681">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1681">username</span></span> |<span data-ttu-id="98caf-1682">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="98caf-1683">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1683">No</span></span> |
| <span data-ttu-id="98caf-1684">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1684">password</span></span> |<span data-ttu-id="98caf-1685">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-1686">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1686">No</span></span> |
| <span data-ttu-id="98caf-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1687">gatewayName</span></span> |<span data-ttu-id="98caf-1688">Имя шлюза hello, hello служба фабрики данных следует использовать базы данных Teradata tooconnect toohello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="98caf-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="98caf-1689">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1690">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="98caf-1691">Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1692">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1692">Dataset</span></span>
<span data-ttu-id="98caf-1693">toodefine набора больших двоичных объектов Teradata hello набор **тип** hello набора данных слишком**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="98caf-1694">В настоящее время нет свойств типа поддерживается для набора данных Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="98caf-1695">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1696">Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-1697">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1698">При копировании данных из базы данных Teradata задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1699">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1699">Property</span></span> | <span data-ttu-id="98caf-1700">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1700">Description</span></span> | <span data-ttu-id="98caf-1701">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1701">Allowed values</span></span> | <span data-ttu-id="98caf-1702">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1703">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1703">query</span></span> |<span data-ttu-id="98caf-1704">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1705">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1705">SQL query string.</span></span> <span data-ttu-id="98caf-1706">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-1707">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1708">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="98caf-1709">Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="98caf-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="98caf-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-1711">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1711">Linked service</span></span>
<span data-ttu-id="98caf-1712">toodefine Cassandra связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesCassandra**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1713">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1713">Property</span></span> | <span data-ttu-id="98caf-1714">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1714">Description</span></span> | <span data-ttu-id="98caf-1715">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1716">host</span><span class="sxs-lookup"><span data-stu-id="98caf-1716">host</span></span> |<span data-ttu-id="98caf-1717">Один или несколько IP-адресов или имен узлов серверов Cassandra.</span><span class="sxs-lookup"><span data-stu-id="98caf-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="98caf-1718">Укажите список разделенных запятой IP-адреса или имена серверов tooall tooconnect одновременно.</span><span class="sxs-lookup"><span data-stu-id="98caf-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="98caf-1719">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1719">Yes</span></span> |
| <span data-ttu-id="98caf-1720">порт</span><span class="sxs-lookup"><span data-stu-id="98caf-1720">port</span></span> |<span data-ttu-id="98caf-1721">TCP-порт, который hello Cassandra server Hello использует toolisten для клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="98caf-1722">Нет. Значение по умолчанию — 9042</span><span class="sxs-lookup"><span data-stu-id="98caf-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="98caf-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1723">authenticationType</span></span> |<span data-ttu-id="98caf-1724">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="98caf-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="98caf-1725">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1725">Yes</span></span> |
| <span data-ttu-id="98caf-1726">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1726">username</span></span> |<span data-ttu-id="98caf-1727">Укажите имя пользователя для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="98caf-1728">Да, если tooBasic authenticationType.</span><span class="sxs-lookup"><span data-stu-id="98caf-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="98caf-1729">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1729">password</span></span> |<span data-ttu-id="98caf-1730">Укажите пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="98caf-1731">Да, если tooBasic authenticationType.</span><span class="sxs-lookup"><span data-stu-id="98caf-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="98caf-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1732">gatewayName</span></span> |<span data-ttu-id="98caf-1733">имя шлюза hello, используемые tooconnect toohello Hello локальной Cassandra базы данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="98caf-1734">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1734">Yes</span></span> |
| <span data-ttu-id="98caf-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-1735">encryptedCredential</span></span> |<span data-ttu-id="98caf-1736">Учетные данные, зашифрованные шлюзом hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="98caf-1737">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1738">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="98caf-1739">Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-1740">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1740">Dataset</span></span>
<span data-ttu-id="98caf-1741">toodefine набора Cassandra hello набор **тип** hello набора данных слишком**CassandraTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1742">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1742">Property</span></span> | <span data-ttu-id="98caf-1743">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1743">Description</span></span> | <span data-ttu-id="98caf-1744">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="98caf-1745">keyspace</span></span> |<span data-ttu-id="98caf-1746">Имя hello пространство ключей или схемы в базе данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="98caf-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="98caf-1747">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="98caf-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-1748">tableName</span></span> |<span data-ttu-id="98caf-1749">Имя таблицы hello Cassandra базы данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="98caf-1750">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1751">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1752">Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="98caf-1753">Источник Cassandra в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1754">При копировании данных из Cassandra задать hello **тип источника** из hello в действии копирования слишком**CassandraSource**и укажите следующие свойства в hello **источника** раздела :</span><span class="sxs-lookup"><span data-stu-id="98caf-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1755">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1755">Property</span></span> | <span data-ttu-id="98caf-1756">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1756">Description</span></span> | <span data-ttu-id="98caf-1757">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1757">Allowed values</span></span> | <span data-ttu-id="98caf-1758">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1759">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1759">query</span></span> |<span data-ttu-id="98caf-1760">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1761">Запрос SQL-92 или CQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="98caf-1762">Ознакомьтесь со [справочником по CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="98caf-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="98caf-1763">При использовании SQL-запрос, укажите **keyspace name.table имя** toorepresent hello таблицу tooquery.</span><span class="sxs-lookup"><span data-stu-id="98caf-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="98caf-1764">Нет (если в наборе данных определены свойства tableName и keyspace)</span><span class="sxs-lookup"><span data-stu-id="98caf-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="98caf-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="98caf-1765">consistencyLevel</span></span> |<span data-ttu-id="98caf-1766">уровень согласованности Hello указывает, сколько реплик должен вернуть запрос чтения tooa до возвращения данных toohello клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="98caf-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="98caf-1767">Проверяет Cassandra hello указанное число реплик, для запроса на чтение данных toosatisfy hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="98caf-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="98caf-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="98caf-1769">Дополнительные сведения см. в статье [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Настройка согласованности данных).</span><span class="sxs-lookup"><span data-stu-id="98caf-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="98caf-1770">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-1770">No.</span></span> <span data-ttu-id="98caf-1771">Значение по умолчанию — ONE</span><span class="sxs-lookup"><span data-stu-id="98caf-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1772">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-1773">Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="98caf-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="98caf-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-1775">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1775">Linked service</span></span>
<span data-ttu-id="98caf-1776">toodefine MongoDB связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesMongoDB**и укажите следующие свойства в hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1777">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1777">Property</span></span> | <span data-ttu-id="98caf-1778">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1778">Description</span></span> | <span data-ttu-id="98caf-1779">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1780">server</span><span class="sxs-lookup"><span data-stu-id="98caf-1780">server</span></span> |<span data-ttu-id="98caf-1781">IP-адрес или имя сервера hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="98caf-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="98caf-1782">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1782">Yes</span></span> |
| <span data-ttu-id="98caf-1783">порт</span><span class="sxs-lookup"><span data-stu-id="98caf-1783">port</span></span> |<span data-ttu-id="98caf-1784">TCP-порт, который hello MongoDB server использует toolisten для клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="98caf-1785">Значение по умолчанию — 27017 (необязательно)</span><span class="sxs-lookup"><span data-stu-id="98caf-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="98caf-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-1786">authenticationType</span></span> |<span data-ttu-id="98caf-1787">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="98caf-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="98caf-1788">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1788">Yes</span></span> |
| <span data-ttu-id="98caf-1789">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-1789">username</span></span> |<span data-ttu-id="98caf-1790">Учетная запись пользователя, tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="98caf-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="98caf-1791">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="98caf-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="98caf-1792">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1792">password</span></span> |<span data-ttu-id="98caf-1793">Пароль для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1793">Password for hello user.</span></span> |<span data-ttu-id="98caf-1794">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="98caf-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="98caf-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="98caf-1795">authSource</span></span> |<span data-ttu-id="98caf-1796">Имя базы данных MongoDB hello, что требуется toouse toocheck учетные данные для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="98caf-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="98caf-1797">Необязательно (если используется обычная проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="98caf-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="98caf-1798">по умолчанию: используется учетная запись администратора hello и hello базы данных, указанный с помощью свойства databaseName.</span><span class="sxs-lookup"><span data-stu-id="98caf-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="98caf-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="98caf-1799">databaseName</span></span> |<span data-ttu-id="98caf-1800">Имя базы данных MongoDB hello, которое следует tooaccess.</span><span class="sxs-lookup"><span data-stu-id="98caf-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="98caf-1801">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1801">Yes</span></span> |
| <span data-ttu-id="98caf-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1802">gatewayName</span></span> |<span data-ttu-id="98caf-1803">Имя шлюза hello, который обращается к хранилищу данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="98caf-1804">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1804">Yes</span></span> |
| <span data-ttu-id="98caf-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-1805">encryptedCredential</span></span> |<span data-ttu-id="98caf-1806">Учетные данные, зашифрованные шлюзом</span><span class="sxs-lookup"><span data-stu-id="98caf-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="98caf-1807">Необязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1808">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="98caf-1809">Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1810">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1810">Dataset</span></span>
<span data-ttu-id="98caf-1811">toodefine набора данных MongoDB hello набор **тип** hello набора данных слишком**MongoDbCollection**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1812">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1812">Property</span></span> | <span data-ttu-id="98caf-1813">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1813">Description</span></span> | <span data-ttu-id="98caf-1814">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="98caf-1815">collectionName</span></span> |<span data-ttu-id="98caf-1816">Имя коллекции hello базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="98caf-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="98caf-1817">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1818">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="98caf-1819">Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="98caf-1820">Источник MongoDB в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1821">При копировании данных из MongoDB задать hello **тип источника** из hello в действии копирования слишком**MongoDbSource**и укажите следующие свойства в hello **источника** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1822">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1822">Property</span></span> | <span data-ttu-id="98caf-1823">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1823">Description</span></span> | <span data-ttu-id="98caf-1824">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1824">Allowed values</span></span> | <span data-ttu-id="98caf-1825">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1826">query</span><span class="sxs-lookup"><span data-stu-id="98caf-1826">query</span></span> |<span data-ttu-id="98caf-1827">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-1828">Строка запроса SQL-92.</span><span class="sxs-lookup"><span data-stu-id="98caf-1828">SQL-92 query string.</span></span> <span data-ttu-id="98caf-1829">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-1830">Нет (если для свойства **collectionName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="98caf-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1831">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1832">Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="98caf-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="98caf-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-1834">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1834">Linked service</span></span>
<span data-ttu-id="98caf-1835">toodefine S3 Amazon связанной службы, набор hello **тип** hello связанной службы слишком**AwsAccessKey**и укажите следующие свойства в hello **typeProperties** раздела :</span><span class="sxs-lookup"><span data-stu-id="98caf-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-1836">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1836">Property</span></span> | <span data-ttu-id="98caf-1837">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1837">Description</span></span> | <span data-ttu-id="98caf-1838">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1838">Allowed values</span></span> | <span data-ttu-id="98caf-1839">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="98caf-1840">accessKeyID</span></span> |<span data-ttu-id="98caf-1841">Идентификатор hello доступа секретного ключа.</span><span class="sxs-lookup"><span data-stu-id="98caf-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="98caf-1842">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1842">string</span></span> |<span data-ttu-id="98caf-1843">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1843">Yes</span></span> |
| <span data-ttu-id="98caf-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="98caf-1844">secretAccessKey</span></span> |<span data-ttu-id="98caf-1845">Hello секретный доступа самого ключа.</span><span class="sxs-lookup"><span data-stu-id="98caf-1845">hello secret access key itself.</span></span> |<span data-ttu-id="98caf-1846">Зашифрованная строка секрета</span><span class="sxs-lookup"><span data-stu-id="98caf-1846">Encrypted secret string</span></span> |<span data-ttu-id="98caf-1847">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-1848">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="98caf-1849">Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1850">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1850">Dataset</span></span>
<span data-ttu-id="98caf-1851">набор данных toodefine S3 Amazon, набор hello **тип** hello набора данных слишком**AmazonS3**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1852">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1852">Property</span></span> | <span data-ttu-id="98caf-1853">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1853">Description</span></span> | <span data-ttu-id="98caf-1854">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1854">Allowed values</span></span> | <span data-ttu-id="98caf-1855">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="98caf-1856">bucketName</span></span> |<span data-ttu-id="98caf-1857">Имя сегмента Hello S3.</span><span class="sxs-lookup"><span data-stu-id="98caf-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="98caf-1858">Строка</span><span class="sxs-lookup"><span data-stu-id="98caf-1858">String</span></span> |<span data-ttu-id="98caf-1859">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1859">Yes</span></span> |
| <span data-ttu-id="98caf-1860">key</span><span class="sxs-lookup"><span data-stu-id="98caf-1860">key</span></span> |<span data-ttu-id="98caf-1861">ключ объекта Hello S3.</span><span class="sxs-lookup"><span data-stu-id="98caf-1861">hello S3 object key.</span></span> |<span data-ttu-id="98caf-1862">Строка</span><span class="sxs-lookup"><span data-stu-id="98caf-1862">String</span></span> |<span data-ttu-id="98caf-1863">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1863">No</span></span> |
| <span data-ttu-id="98caf-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="98caf-1864">prefix</span></span> |<span data-ttu-id="98caf-1865">Префикс для ключа объекта S3 hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="98caf-1866">Выбираются объекты, ключи которых начинаются с этого префикса.</span><span class="sxs-lookup"><span data-stu-id="98caf-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="98caf-1867">Применяется, только если ключ пустой.</span><span class="sxs-lookup"><span data-stu-id="98caf-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="98caf-1868">string</span><span class="sxs-lookup"><span data-stu-id="98caf-1868">String</span></span> |<span data-ttu-id="98caf-1869">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1869">No</span></span> |
| <span data-ttu-id="98caf-1870">версия</span><span class="sxs-lookup"><span data-stu-id="98caf-1870">version</span></span> |<span data-ttu-id="98caf-1871">версия Hello объекта S3, если включено управление версиями S3.</span><span class="sxs-lookup"><span data-stu-id="98caf-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="98caf-1872">Строка</span><span class="sxs-lookup"><span data-stu-id="98caf-1872">String</span></span> |<span data-ttu-id="98caf-1873">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1873">No</span></span> |
| <span data-ttu-id="98caf-1874">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-1874">format</span></span> | <span data-ttu-id="98caf-1875">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-1876">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-1877">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-1878">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-1879">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1879">No</span></span> | |
| <span data-ttu-id="98caf-1880">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-1880">compression</span></span> | <span data-ttu-id="98caf-1881">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-1882">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98caf-1883">уровни Hello поддерживается: **оптимальный** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-1884">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-1885">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="98caf-1886">bucketName + клавиша указывает расположение hello объекта hello S3 где контейнеров — hello корневой контейнер для объектов S3 и нажата клавиша объекта tooS3 hello полный путь.</span><span class="sxs-lookup"><span data-stu-id="98caf-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="98caf-1887">Пример: пример набора данных с префиксом</span><span class="sxs-lookup"><span data-stu-id="98caf-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="98caf-1888">Пример: пример набора данных (с версией)</span><span class="sxs-lookup"><span data-stu-id="98caf-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="98caf-1889">Пример: динамические пути для S3</span><span class="sxs-lookup"><span data-stu-id="98caf-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="98caf-1890">В образце hello мы используем фиксированные значения для свойств ключа и bucketName в наборе данных hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="98caf-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="98caf-1891">Может иметь вычисления ключа hello и bucketName динамически во время выполнения с помощью системных переменных, например SliceStart фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="98caf-1892">Можно сделать hello же hello префикс свойства набора данных Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="98caf-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="98caf-1893">В статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md) приведен список поддерживаемых функций и переменных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="98caf-1894">Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="98caf-1895">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1896">При копировании данных из Amazon S3 задать hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздела :</span><span class="sxs-lookup"><span data-stu-id="98caf-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="98caf-1897">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1897">Property</span></span> | <span data-ttu-id="98caf-1898">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1898">Description</span></span> | <span data-ttu-id="98caf-1899">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1899">Allowed values</span></span> | <span data-ttu-id="98caf-1900">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-1901">recursive</span></span> |<span data-ttu-id="98caf-1902">Указывает объекты ли список toorecursively S3 hello в каталоге.</span><span class="sxs-lookup"><span data-stu-id="98caf-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="98caf-1903">True или false</span><span class="sxs-lookup"><span data-stu-id="98caf-1903">true/false</span></span> |<span data-ttu-id="98caf-1904">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="98caf-1905">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="98caf-1906">Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="98caf-1907">Файловая система</span><span class="sxs-lookup"><span data-stu-id="98caf-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-1908">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1908">Linked service</span></span>
<span data-ttu-id="98caf-1909">Можно связать локального файла tooan данных Azure заводе hello **файловый сервер в локальной** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="98caf-1910">Привет, в следующей таблице приводится описание JSON элементы, которые являются определенной toohello файловый сервер в локальной связанной службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="98caf-1911">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1911">Property</span></span> | <span data-ttu-id="98caf-1912">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1912">Description</span></span> | <span data-ttu-id="98caf-1913">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1914">type</span><span class="sxs-lookup"><span data-stu-id="98caf-1914">type</span></span> |<span data-ttu-id="98caf-1915">Убедитесь, что свойство типа hello слишком**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="98caf-1916">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1916">Yes</span></span> |
| <span data-ttu-id="98caf-1917">host</span><span class="sxs-lookup"><span data-stu-id="98caf-1917">host</span></span> |<span data-ttu-id="98caf-1918">Указывает путь к корневому каталогу hello hello папке, что toocopy.</span><span class="sxs-lookup"><span data-stu-id="98caf-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="98caf-1919">Использовать hello escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="98caf-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="98caf-1920">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="98caf-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="98caf-1921">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1921">Yes</span></span> |
| <span data-ttu-id="98caf-1922">userid</span><span class="sxs-lookup"><span data-stu-id="98caf-1922">userid</span></span> |<span data-ttu-id="98caf-1923">Укажите идентификатор hello hello пользователя, имеющего доступ toohello сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="98caf-1924">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="98caf-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="98caf-1925">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-1925">password</span></span> |<span data-ttu-id="98caf-1926">Задать пароль hello hello пользователя (userid).</span><span class="sxs-lookup"><span data-stu-id="98caf-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="98caf-1927">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="98caf-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="98caf-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-1928">encryptedCredential</span></span> |<span data-ttu-id="98caf-1929">Укажите hello зашифрованные учетные данные, которые можно получить, выполнив командлет New-AzureRmDataFactoryEncryptValue hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="98caf-1930">Нет (Если вы выберете toospecify идентификатор пользователя и пароль в виде обычного текста)</span><span class="sxs-lookup"><span data-stu-id="98caf-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="98caf-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-1931">gatewayName</span></span> |<span data-ttu-id="98caf-1932">Указывает имя фабрики данных для использования локального файла tooconnect toohello сервера шлюза hello hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="98caf-1933">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="98caf-1934">Пример определений пути к папке</span><span class="sxs-lookup"><span data-stu-id="98caf-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="98caf-1935">Сценарий</span><span class="sxs-lookup"><span data-stu-id="98caf-1935">Scenario</span></span> | <span data-ttu-id="98caf-1936">Размещение в определении связанной службы</span><span class="sxs-lookup"><span data-stu-id="98caf-1936">Host in linked service definition</span></span> | <span data-ttu-id="98caf-1937">Путь к файлу в определении набора данных</span><span class="sxs-lookup"><span data-stu-id="98caf-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1938">Локальная папка на компьютере со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="98caf-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="98caf-1939">Примеры: "D:\\\\*" или "D:\папка\вложенная_папка\\\*"</span><span class="sxs-lookup"><span data-stu-id="98caf-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="98caf-1940">"D:\\\\" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="98caf-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="98caf-1941">localhost (для версий, предшествующих версии 2.0 шлюза управления данными)</span><span class="sxs-lookup"><span data-stu-id="98caf-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="98caf-1942">.\\\\ или "папка\\\\вложенная_папка" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="98caf-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="98caf-1943">"D:\\\\" или "D:\\\\папка\\\\вложенная_папка" (для шлюза версии ниже 2.0)</span><span class="sxs-lookup"><span data-stu-id="98caf-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="98caf-1944">Удаленная общая папка:</span><span class="sxs-lookup"><span data-stu-id="98caf-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="98caf-1945">Примеры: "\\\\сервер\\общая_папка\\\*" или "\\\\сервер\\общая_папка\\папка\\вложенная_папка\\*"</span><span class="sxs-lookup"><span data-stu-id="98caf-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="98caf-1946">\\\\\\\\сервер\\\\общая_папка</span><span class="sxs-lookup"><span data-stu-id="98caf-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="98caf-1947">.\\\\ или "папка\\\\вложенная_папка"</span><span class="sxs-lookup"><span data-stu-id="98caf-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="98caf-1948">Пример указания имени пользователя и пароля в виде обычного текста</span><span class="sxs-lookup"><span data-stu-id="98caf-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="98caf-1949">Пример использования encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="98caf-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="98caf-1950">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-1951">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-1951">Dataset</span></span>
<span data-ttu-id="98caf-1952">toodefine набора данных файловой системы, набор hello **тип** hello набора данных слишком**общей папкой**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-1953">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1953">Property</span></span> | <span data-ttu-id="98caf-1954">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1954">Description</span></span> | <span data-ttu-id="98caf-1955">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="98caf-1956">folderPath</span></span> |<span data-ttu-id="98caf-1957">Указывает папку toohello вложенным hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="98caf-1958">Использовать hello escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="98caf-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="98caf-1959">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="98caf-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="98caf-1960">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="98caf-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="98caf-1961">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-1961">Yes</span></span> |
| <span data-ttu-id="98caf-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="98caf-1962">fileName</span></span> |<span data-ttu-id="98caf-1963">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="98caf-1964">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="98caf-1965">Если имя файла не указано для выходной набор данных, hello hello созданный файл называется в кодировке hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="98caf-1966">`Data.<Guid>.txt` (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="98caf-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="98caf-1967">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1967">No</span></span> |
| <span data-ttu-id="98caf-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="98caf-1968">fileFilter</span></span> |<span data-ttu-id="98caf-1969">Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.</span><span class="sxs-lookup"><span data-stu-id="98caf-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="98caf-1970">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="98caf-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="98caf-1971">Пример 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="98caf-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="98caf-1972">Пример 2: fileFilter: 2016-1-?.txt</span><span class="sxs-lookup"><span data-stu-id="98caf-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="98caf-1973">Обратите внимание, что свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="98caf-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="98caf-1974">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1974">No</span></span> |
| <span data-ttu-id="98caf-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="98caf-1975">partitionedBy</span></span> |<span data-ttu-id="98caf-1976">PartitionedBy toospecify динамический folderPath и fileName можно использовать для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="98caf-1977">Например, можно параметризовать значение folderPath для каждого часа получения данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="98caf-1978">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1978">No</span></span> |
| <span data-ttu-id="98caf-1979">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-1979">format</span></span> | <span data-ttu-id="98caf-1980">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-1981">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-1982">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-1983">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-1984">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1984">No</span></span> |
| <span data-ttu-id="98caf-1985">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-1985">compression</span></span> | <span data-ttu-id="98caf-1986">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-1987">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-1988">См. сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-1989">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="98caf-1990">Свойства filename и fileFilter невозможно использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="98caf-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-1991">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-1992">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="98caf-1993">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="98caf-1994">При копировании данных из файловой системы, задайте hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-1995">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-1995">Property</span></span> | <span data-ttu-id="98caf-1996">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-1996">Description</span></span> | <span data-ttu-id="98caf-1997">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-1997">Allowed values</span></span> | <span data-ttu-id="98caf-1998">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-1999">recursive</span></span> |<span data-ttu-id="98caf-2000">Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello или только пользователей из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="98caf-2001">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-2001">True, False (default)</span></span> |<span data-ttu-id="98caf-2002">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2003">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="98caf-2004">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="98caf-2005">Приемник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="98caf-2006">При копировании данных tooFile системы задать hello **тип приемника** из hello в действии копирования слишком**FileSystemSink**и укажите следующие свойства в hello **приемник** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="98caf-2007">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2007">Property</span></span> | <span data-ttu-id="98caf-2008">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2008">Description</span></span> | <span data-ttu-id="98caf-2009">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-2009">Allowed values</span></span> | <span data-ttu-id="98caf-2010">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="98caf-2011">copyBehavior</span></span> |<span data-ttu-id="98caf-2012">Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы.</span><span class="sxs-lookup"><span data-stu-id="98caf-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="98caf-2013">**PreserveHierarchy:** сохраняет hello иерархию файлов в целевой папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="98caf-2014">То есть относительный путь hello hello исходный файл toohello исходную папку hello такой же, как относительный путь hello hello целевой файл toohello целевую папку.</span><span class="sxs-lookup"><span data-stu-id="98caf-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="98caf-2015">**FlattenHierarchy:** все файлы из исходной папки hello создаются в первый уровень hello целевую папку.</span><span class="sxs-lookup"><span data-stu-id="98caf-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="98caf-2016">Hello целевые файлы создаются с автоматически созданным именем.</span><span class="sxs-lookup"><span data-stu-id="98caf-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="98caf-2017">**MergeFiles:** объединяет все файлы из папки tooone hello исходного файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="98caf-2018">Если указано имя BLOB-объекта или имени файла hello hello объединенный файл называется hello указанным именем.</span><span class="sxs-lookup"><span data-stu-id="98caf-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="98caf-2019">В противном случае присваивается автоматически созданное имя файла.</span><span class="sxs-lookup"><span data-stu-id="98caf-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="98caf-2020">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2020">No</span></span> |
<span data-ttu-id="98caf-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="98caf-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-2022">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-2023">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="98caf-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="98caf-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-2025">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2025">Linked service</span></span>
<span data-ttu-id="98caf-2026">toodefine FTP связанной службы, набор hello **тип** hello связанной службы слишком**FTP-сервер**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2027">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2027">Property</span></span> | <span data-ttu-id="98caf-2028">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2028">Description</span></span> | <span data-ttu-id="98caf-2029">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2029">Required</span></span> | <span data-ttu-id="98caf-2030">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="98caf-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2031">host</span><span class="sxs-lookup"><span data-stu-id="98caf-2031">host</span></span> |<span data-ttu-id="98caf-2032">Имя или IP-адрес FTP-сервера hello</span><span class="sxs-lookup"><span data-stu-id="98caf-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="98caf-2033">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="98caf-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2034">authenticationType</span></span> |<span data-ttu-id="98caf-2035">Укажите тип аутентификации</span><span class="sxs-lookup"><span data-stu-id="98caf-2035">Specify authentication type</span></span> |<span data-ttu-id="98caf-2036">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2036">Yes</span></span> |<span data-ttu-id="98caf-2037">Обычная, анонимная</span><span class="sxs-lookup"><span data-stu-id="98caf-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="98caf-2038">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2038">username</span></span> |<span data-ttu-id="98caf-2039">Пользователь, имеющий доступ toohello FTP сервера</span><span class="sxs-lookup"><span data-stu-id="98caf-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="98caf-2040">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="98caf-2041">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2041">password</span></span> |<span data-ttu-id="98caf-2042">Пароль для пользователя hello (имя пользователя)</span><span class="sxs-lookup"><span data-stu-id="98caf-2042">Password for hello user (username)</span></span> |<span data-ttu-id="98caf-2043">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="98caf-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-2044">encryptedCredential</span></span> |<span data-ttu-id="98caf-2045">Зашифрованных учетных данных tooaccess hello FTP-сервера</span><span class="sxs-lookup"><span data-stu-id="98caf-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="98caf-2046">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="98caf-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2047">gatewayName</span></span> |<span data-ttu-id="98caf-2048">Имя шлюза tooconnect hello шлюз управления данными tooan локальной FTP-сервера</span><span class="sxs-lookup"><span data-stu-id="98caf-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="98caf-2049">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="98caf-2050">порт</span><span class="sxs-lookup"><span data-stu-id="98caf-2050">port</span></span> |<span data-ttu-id="98caf-2051">Какие hello FTP сервера прослушивает порт</span><span class="sxs-lookup"><span data-stu-id="98caf-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="98caf-2052">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2052">No</span></span> |<span data-ttu-id="98caf-2053">21</span><span class="sxs-lookup"><span data-stu-id="98caf-2053">21</span></span> |
| <span data-ttu-id="98caf-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="98caf-2054">enableSsl</span></span> |<span data-ttu-id="98caf-2055">Укажите, является ли toouse FTP через канал SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="98caf-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="98caf-2056">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2056">No</span></span> |<span data-ttu-id="98caf-2057">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2057">true</span></span> |
| <span data-ttu-id="98caf-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="98caf-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="98caf-2059">Укажите, является ли сервер tooenable SSL проверку сертификата при использовании FTP по каналу SSL/TLS</span><span class="sxs-lookup"><span data-stu-id="98caf-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="98caf-2060">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2060">No</span></span> |<span data-ttu-id="98caf-2061">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="98caf-2062">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="98caf-2063">Пример: использование имени пользователя и пароля в виде обычного текста для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="98caf-2064">Пример: использование свойств port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="98caf-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="98caf-2065">Пример: использование свойства encryptedCredential для проверки подлинности и шлюза</span><span class="sxs-lookup"><span data-stu-id="98caf-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="98caf-2066">Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-2067">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2067">Dataset</span></span>
<span data-ttu-id="98caf-2068">toodefine FTP набора данных, набор hello **тип** hello набора данных слишком**FileShare**и укажите следующие свойства в hello hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2069">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2069">Property</span></span> | <span data-ttu-id="98caf-2070">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2070">Description</span></span> | <span data-ttu-id="98caf-2071">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="98caf-2072">folderPath</span></span> |<span data-ttu-id="98caf-2073">Путь toohello вложенной папкой.</span><span class="sxs-lookup"><span data-stu-id="98caf-2073">Sub path toohello folder.</span></span> <span data-ttu-id="98caf-2074">Использовать escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="98caf-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="98caf-2075">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="98caf-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="98caf-2076">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="98caf-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="98caf-2077">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2077">Yes</span></span> 
| <span data-ttu-id="98caf-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="98caf-2078">fileName</span></span> |<span data-ttu-id="98caf-2079">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="98caf-2080">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="98caf-2081">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="98caf-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="98caf-2082">Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="98caf-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="98caf-2083">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2083">No</span></span> |
| <span data-ttu-id="98caf-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="98caf-2084">fileFilter</span></span> |<span data-ttu-id="98caf-2085">Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.</span><span class="sxs-lookup"><span data-stu-id="98caf-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="98caf-2086">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="98caf-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="98caf-2087">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="98caf-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="98caf-2088">Пример 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="98caf-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="98caf-2089">Свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="98caf-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="98caf-2090">HDFS не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="98caf-2091">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2091">No</span></span> |
| <span data-ttu-id="98caf-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="98caf-2092">partitionedBy</span></span> |<span data-ttu-id="98caf-2093">partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="98caf-2094">Например, путь к папке folderPath каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="98caf-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="98caf-2095">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2095">No</span></span> |
| <span data-ttu-id="98caf-2096">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-2096">format</span></span> | <span data-ttu-id="98caf-2097">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-2098">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-2099">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-2100">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-2101">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2101">No</span></span> |
| <span data-ttu-id="98caf-2102">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-2102">compression</span></span> | <span data-ttu-id="98caf-2103">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-2104">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-2105">Узнайте больше о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-2106">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2106">No</span></span> |
| <span data-ttu-id="98caf-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="98caf-2107">useBinaryTransfer</span></span> |<span data-ttu-id="98caf-2108">Укажите, использовать ли режим передачи в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="98caf-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="98caf-2109">Значение true, если использовать двоичный режим, и false, если ASCII.</span><span class="sxs-lookup"><span data-stu-id="98caf-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="98caf-2110">Значение по умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="98caf-2110">Default value: True.</span></span> <span data-ttu-id="98caf-2111">Это свойство можно использовать, только когда тип связанной службы является FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="98caf-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="98caf-2112">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="98caf-2113">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-2114">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="98caf-2115">Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="98caf-2116">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2117">При копировании данных с сервера FTP, задайте hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-2118">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2118">Property</span></span> | <span data-ttu-id="98caf-2119">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2119">Description</span></span> | <span data-ttu-id="98caf-2120">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-2120">Allowed values</span></span> | <span data-ttu-id="98caf-2121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-2122">recursive</span></span> |<span data-ttu-id="98caf-2123">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="98caf-2124">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-2124">True, False (default)</span></span> |<span data-ttu-id="98caf-2125">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2126">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="98caf-2127">Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="98caf-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="98caf-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-2129">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2129">Linked service</span></span>
<span data-ttu-id="98caf-2130">toodefine HDFS связанной службы, набор hello **тип** hello связанной службы слишком**Hdfs**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2131">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2131">Property</span></span> | <span data-ttu-id="98caf-2132">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2132">Description</span></span> | <span data-ttu-id="98caf-2133">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2134">type</span><span class="sxs-lookup"><span data-stu-id="98caf-2134">type</span></span> |<span data-ttu-id="98caf-2135">свойство типа Hello должно быть присвоено: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="98caf-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="98caf-2136">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2136">Yes</span></span> |
| <span data-ttu-id="98caf-2137">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="98caf-2137">Url</span></span> |<span data-ttu-id="98caf-2138">URL-адрес toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="98caf-2138">URL toohello HDFS</span></span> |<span data-ttu-id="98caf-2139">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2139">Yes</span></span> |
| <span data-ttu-id="98caf-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2140">authenticationType</span></span> |<span data-ttu-id="98caf-2141">Anonymous или Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="98caf-2142">toouse **проверки подлинности Kerberos** HDFS соединителя, см. в разделе слишком[в этом разделе](#use-kerberos-authentication-for-hdfs-connector) tooset вверх в локальной среде соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="98caf-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="98caf-2143">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2143">Yes</span></span> |
| <span data-ttu-id="98caf-2144">userName</span><span class="sxs-lookup"><span data-stu-id="98caf-2144">userName</span></span> |<span data-ttu-id="98caf-2145">Имя пользователя для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="98caf-2146">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="98caf-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="98caf-2147">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2147">password</span></span> |<span data-ttu-id="98caf-2148">Пароль для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="98caf-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="98caf-2149">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="98caf-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="98caf-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2150">gatewayName</span></span> |<span data-ttu-id="98caf-2151">Имя шлюза hello, hello служба фабрики данных следует использовать tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="98caf-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="98caf-2152">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2152">Yes</span></span> |
| <span data-ttu-id="98caf-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-2153">encryptedCredential</span></span> |<span data-ttu-id="98caf-2154">[Новый AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) выходных данных учетные данные доступа hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="98caf-2155">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="98caf-2156">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="98caf-2157">Пример: использование проверки подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="98caf-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="98caf-2158">Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-2159">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2159">Dataset</span></span>
<span data-ttu-id="98caf-2160">toodefine набора HDFS hello набор **тип** hello набора данных слишком**FileShare**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2161">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2161">Property</span></span> | <span data-ttu-id="98caf-2162">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2162">Description</span></span> | <span data-ttu-id="98caf-2163">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="98caf-2164">folderPath</span></span> |<span data-ttu-id="98caf-2165">Путь к папке toohello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2165">Path toohello folder.</span></span> <span data-ttu-id="98caf-2166">Пример: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="98caf-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="98caf-2167">Использовать escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="98caf-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="98caf-2168">Например, для "папка\вложенная_папка" укажите "папка\\\\вложенная_папка", а для "d:\пример_папки" укажите "d:\\\\пример_папки".</span><span class="sxs-lookup"><span data-stu-id="98caf-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="98caf-2169">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="98caf-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="98caf-2170">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2170">Yes</span></span> |
| <span data-ttu-id="98caf-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="98caf-2171">fileName</span></span> |<span data-ttu-id="98caf-2172">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="98caf-2173">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="98caf-2174">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="98caf-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="98caf-2175">Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="98caf-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="98caf-2176">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2176">No</span></span> |
| <span data-ttu-id="98caf-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="98caf-2177">partitionedBy</span></span> |<span data-ttu-id="98caf-2178">partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="98caf-2179">Например, путь к папке (folderPath) каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="98caf-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="98caf-2180">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2180">No</span></span> |
| <span data-ttu-id="98caf-2181">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-2181">format</span></span> | <span data-ttu-id="98caf-2182">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-2183">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-2184">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-2185">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-2186">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2186">No</span></span> |
| <span data-ttu-id="98caf-2187">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-2187">compression</span></span> | <span data-ttu-id="98caf-2188">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-2189">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98caf-2190">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-2191">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-2192">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="98caf-2193">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-2194">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="98caf-2195">Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="98caf-2196">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2197">При копировании данных из HDFS задать hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="98caf-2198">**FileSystemSource** поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="98caf-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="98caf-2199">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2199">Property</span></span> | <span data-ttu-id="98caf-2200">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2200">Description</span></span> | <span data-ttu-id="98caf-2201">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-2201">Allowed values</span></span> | <span data-ttu-id="98caf-2202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-2203">recursive</span></span> |<span data-ttu-id="98caf-2204">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="98caf-2205">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-2205">True, False (default)</span></span> |<span data-ttu-id="98caf-2206">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2207">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="98caf-2208">Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="98caf-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="98caf-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-2210">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2210">Linked service</span></span>
<span data-ttu-id="98caf-2211">toodefine SFTP связанной службы, набор hello **тип** hello связанной службы слишком**Sftp**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2212">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2212">Property</span></span> | <span data-ttu-id="98caf-2213">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2213">Description</span></span> | <span data-ttu-id="98caf-2214">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2215">host</span><span class="sxs-lookup"><span data-stu-id="98caf-2215">host</span></span> | <span data-ttu-id="98caf-2216">Имя или IP-адрес SFTP-сервере hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="98caf-2217">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2217">Yes</span></span> |
| <span data-ttu-id="98caf-2218">порт</span><span class="sxs-lookup"><span data-stu-id="98caf-2218">port</span></span> |<span data-ttu-id="98caf-2219">Какие hello SFTP сервера прослушивает порт.</span><span class="sxs-lookup"><span data-stu-id="98caf-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="98caf-2220">значение по умолчанию Hello: 21</span><span class="sxs-lookup"><span data-stu-id="98caf-2220">hello default value is: 21</span></span> |<span data-ttu-id="98caf-2221">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2221">No</span></span> |
| <span data-ttu-id="98caf-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2222">authenticationType</span></span> |<span data-ttu-id="98caf-2223">Укажите тип аутентификации.</span><span class="sxs-lookup"><span data-stu-id="98caf-2223">Specify authentication type.</span></span> <span data-ttu-id="98caf-2224">Допустимые значения: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="98caf-2225">См. слишком[использование обычной проверки подлинности](#using-basic-authentication) и [с помощью открытого ключа проверки подлинности SSH](#using-ssh-public-key-authentication) разделы в дополнительные свойства и примерами JSON, соответственно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="98caf-2226">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2226">Yes</span></span> |
| <span data-ttu-id="98caf-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="98caf-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="98caf-2228">Укажите, размещена ли tooskip ключа проверки.</span><span class="sxs-lookup"><span data-stu-id="98caf-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="98caf-2229">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-2229">No.</span></span> <span data-ttu-id="98caf-2230">Здравствуйте, значение по умолчанию: false</span><span class="sxs-lookup"><span data-stu-id="98caf-2230">hello default value: false</span></span> |
| <span data-ttu-id="98caf-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="98caf-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="98caf-2232">Укажите отпечаток пальца hello hello узла ключа.</span><span class="sxs-lookup"><span data-stu-id="98caf-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="98caf-2233">Да, если hello `skipHostKeyValidation` имеет значение toofalse.</span><span class="sxs-lookup"><span data-stu-id="98caf-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="98caf-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2234">gatewayName</span></span> |<span data-ttu-id="98caf-2235">Имя tooan tooconnect шлюз управления данными hello локальной SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="98caf-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="98caf-2236">Да, если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="98caf-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-2237">encryptedCredential</span></span> | <span data-ttu-id="98caf-2238">Сервер SFTP hello tooaccess зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="98caf-2239">Формируется автоматически при указании обычной проверки подлинности (имя пользователя + пароль) или параметры SshPublicKey проверки подлинности (имя пользователя + пути закрытого ключа или содержимое) в копирования мастера или hello ClickOnce всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="98caf-2240">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-2240">No.</span></span> <span data-ttu-id="98caf-2241">Применимо, только если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="98caf-2242">Пример: использование обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="98caf-2243">Задайте обычную проверку подлинности toouse `authenticationType` как `Basic`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="98caf-2244">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2244">Property</span></span> | <span data-ttu-id="98caf-2245">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2245">Description</span></span> | <span data-ttu-id="98caf-2246">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2247">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2247">username</span></span> | <span data-ttu-id="98caf-2248">Пользователь, обладающий доступом toohello SFTP-сервере.</span><span class="sxs-lookup"><span data-stu-id="98caf-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="98caf-2249">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2249">Yes</span></span> |
| <span data-ttu-id="98caf-2250">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2250">password</span></span> | <span data-ttu-id="98caf-2251">Пароль для пользователя hello (имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="98caf-2251">Password for hello user (username).</span></span> | <span data-ttu-id="98caf-2252">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="98caf-2253">Пример: обычная проверка подлинности с шифрованием учетных данных**</span><span class="sxs-lookup"><span data-stu-id="98caf-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="98caf-2254">Пример: использование проверки подлинности с открытым ключом SSH**</span><span class="sxs-lookup"><span data-stu-id="98caf-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="98caf-2255">Задайте обычную проверку подлинности toouse `authenticationType` как `SshPublicKey`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="98caf-2256">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2256">Property</span></span> | <span data-ttu-id="98caf-2257">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2257">Description</span></span> | <span data-ttu-id="98caf-2258">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2259">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2259">username</span></span> |<span data-ttu-id="98caf-2260">Пользователь, имеющий доступ toohello SFTP-сервера</span><span class="sxs-lookup"><span data-stu-id="98caf-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="98caf-2261">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2261">Yes</span></span> |
| <span data-ttu-id="98caf-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="98caf-2262">privateKeyPath</span></span> | <span data-ttu-id="98caf-2263">Укажите абсолютный путь toohello можно получить доступ к файлу закрытого ключа этого шлюза.</span><span class="sxs-lookup"><span data-stu-id="98caf-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="98caf-2264">Укажите либо hello `privateKeyPath` или `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="98caf-2265">Применимо, только если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="98caf-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="98caf-2266">privateKeyContent</span></span> | <span data-ttu-id="98caf-2267">Сериализованная строка hello закрытого ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="98caf-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="98caf-2268">Hello мастер копирования можно считать файл закрытого ключа hello и автоматически извлекать hello закрытого ключа содержимого.</span><span class="sxs-lookup"><span data-stu-id="98caf-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="98caf-2269">При использовании любой другой инструмент и SDK, используйте свойство privateKeyPath hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="98caf-2270">Укажите либо hello `privateKeyPath` или `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="98caf-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="98caf-2271">passPhrase</span></span> | <span data-ttu-id="98caf-2272">Укажите фразу пароль toodecrypt hello hello закрытый ключ, если hello файл ключа защищен парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="98caf-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="98caf-2273">Да, если файл закрытого ключа hello защищен парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="98caf-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="98caf-2274">Пример: проверка подлинности с закрытым ключом SSH, для которого указано содержимое**</span><span class="sxs-lookup"><span data-stu-id="98caf-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="98caf-2275">Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-2276">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2276">Dataset</span></span>
<span data-ttu-id="98caf-2277">toodefine набор SFTP hello набор **тип** hello набора данных слишком**FileShare**и укажите следующие свойства в hello hello **typeProperties** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2278">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2278">Property</span></span> | <span data-ttu-id="98caf-2279">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2279">Description</span></span> | <span data-ttu-id="98caf-2280">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="98caf-2281">folderPath</span></span> |<span data-ttu-id="98caf-2282">Путь toohello вложенной папкой.</span><span class="sxs-lookup"><span data-stu-id="98caf-2282">Sub path toohello folder.</span></span> <span data-ttu-id="98caf-2283">Использовать escape-символ "\" для специальных символов в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="98caf-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="98caf-2284">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="98caf-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="98caf-2285">Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="98caf-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="98caf-2286">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2286">Yes</span></span> |
| <span data-ttu-id="98caf-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="98caf-2287">fileName</span></span> |<span data-ttu-id="98caf-2288">Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="98caf-2289">Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="98caf-2290">Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="98caf-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="98caf-2291">Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="98caf-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="98caf-2292">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2292">No</span></span> |
| <span data-ttu-id="98caf-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="98caf-2293">fileFilter</span></span> |<span data-ttu-id="98caf-2294">Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.</span><span class="sxs-lookup"><span data-stu-id="98caf-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="98caf-2295">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="98caf-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="98caf-2296">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="98caf-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="98caf-2297">Пример 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="98caf-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="98caf-2298">Свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="98caf-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="98caf-2299">HDFS не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="98caf-2300">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2300">No</span></span> |
| <span data-ttu-id="98caf-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="98caf-2301">partitionedBy</span></span> |<span data-ttu-id="98caf-2302">partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="98caf-2303">Например, путь к папке folderPath каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="98caf-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="98caf-2304">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2304">No</span></span> |
| <span data-ttu-id="98caf-2305">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-2305">format</span></span> | <span data-ttu-id="98caf-2306">поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-2307">Набор hello **тип** свойства в формате tooone из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="98caf-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="98caf-2308">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98caf-2309">Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98caf-2310">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2310">No</span></span> |
| <span data-ttu-id="98caf-2311">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-2311">compression</span></span> | <span data-ttu-id="98caf-2312">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-2313">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98caf-2314">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-2315">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-2316">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2316">No</span></span> |
| <span data-ttu-id="98caf-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="98caf-2317">useBinaryTransfer</span></span> |<span data-ttu-id="98caf-2318">Укажите, использовать ли режим передачи в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="98caf-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="98caf-2319">Значение true, если использовать двоичный режим, и false, если ASCII.</span><span class="sxs-lookup"><span data-stu-id="98caf-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="98caf-2320">Значение по умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="98caf-2320">Default value: True.</span></span> <span data-ttu-id="98caf-2321">Это свойство можно использовать, только когда тип связанной службы является FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="98caf-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="98caf-2322">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="98caf-2323">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-2324">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="98caf-2325">Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="98caf-2326">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2327">При копировании данных из источника SFTP задать hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-2328">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2328">Property</span></span> | <span data-ttu-id="98caf-2329">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2329">Description</span></span> | <span data-ttu-id="98caf-2330">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-2330">Allowed values</span></span> | <span data-ttu-id="98caf-2331">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="98caf-2332">recursive</span></span> |<span data-ttu-id="98caf-2333">Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="98caf-2334">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-2334">True, False (default)</span></span> |<span data-ttu-id="98caf-2335">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="98caf-2336">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="98caf-2337">Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="98caf-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="98caf-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-2339">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2339">Linked service</span></span>
<span data-ttu-id="98caf-2340">toodefine HTTP связанной службы, набор hello **тип** hello связанной службы слишком**Http**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2341">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2341">Property</span></span> | <span data-ttu-id="98caf-2342">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2342">Description</span></span> | <span data-ttu-id="98caf-2343">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2344">url</span><span class="sxs-lookup"><span data-stu-id="98caf-2344">url</span></span> | <span data-ttu-id="98caf-2345">Базовый URL-адрес toohello веб-сервера</span><span class="sxs-lookup"><span data-stu-id="98caf-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="98caf-2346">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2346">Yes</span></span> |
| <span data-ttu-id="98caf-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2347">authenticationType</span></span> | <span data-ttu-id="98caf-2348">Указывает тип проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="98caf-2349">Допустимые значения: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="98caf-2350">Относятся toosections под этой таблицей в дополнительные свойства и примерами JSON для этих типов проверки подлинности, соответственно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="98caf-2351">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2351">Yes</span></span> |
| <span data-ttu-id="98caf-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="98caf-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="98caf-2353">Укажите ли tooenable сервера SSL сертификата проверки, если источником является HTTPS веб-сервера</span><span class="sxs-lookup"><span data-stu-id="98caf-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="98caf-2354">Нет. Значение по умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="98caf-2354">No, default is true</span></span> |
| <span data-ttu-id="98caf-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2355">gatewayName</span></span> | <span data-ttu-id="98caf-2356">Имя tooan tooconnect шлюз управления данными hello локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="98caf-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="98caf-2357">Да, если копирование выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="98caf-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="98caf-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-2358">encryptedCredential</span></span> | <span data-ttu-id="98caf-2359">Конечная точка HTTP hello tooaccess зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="98caf-2360">Автоматически сгенерированный при настройке hello сведения для проверки подлинности в копирования мастера или hello ClickOnce всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="98caf-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="98caf-2361">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-2361">No.</span></span> <span data-ttu-id="98caf-2362">Применимо, только когда копирование данных выполняется с локального HTTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="98caf-2363">Пример: использование типов проверки подлинности Basic, Digest или Windows</span><span class="sxs-lookup"><span data-stu-id="98caf-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="98caf-2364">Задать `authenticationType` как `Basic`, `Digest`, или `Windows`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="98caf-2365">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2365">Property</span></span> | <span data-ttu-id="98caf-2366">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2366">Description</span></span> | <span data-ttu-id="98caf-2367">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2368">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2368">username</span></span> | <span data-ttu-id="98caf-2369">Конечная точка HTTP hello tooaccess имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="98caf-2370">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2370">Yes</span></span> |
| <span data-ttu-id="98caf-2371">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2371">password</span></span> | <span data-ttu-id="98caf-2372">Пароль для пользователя hello (имя пользователя).</span><span class="sxs-lookup"><span data-stu-id="98caf-2372">Password for hello user (username).</span></span> | <span data-ttu-id="98caf-2373">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="98caf-2374">Пример: использование типа проверки подлинности ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="98caf-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="98caf-2375">Задайте обычную проверку подлинности toouse `authenticationType` как `ClientCertificate`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:</span><span class="sxs-lookup"><span data-stu-id="98caf-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="98caf-2376">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2376">Property</span></span> | <span data-ttu-id="98caf-2377">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2377">Description</span></span> | <span data-ttu-id="98caf-2378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="98caf-2379">embeddedCertData</span></span> | <span data-ttu-id="98caf-2380">Hello кодировке Base64 содержимое двоичных данных hello файл обмена личной информацией (PFX).</span><span class="sxs-lookup"><span data-stu-id="98caf-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="98caf-2381">Укажите либо hello `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="98caf-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="98caf-2382">certThumbprint</span></span> | <span data-ttu-id="98caf-2383">Здравствуйте, отпечаток сертификата hello, который был установлен в хранилище сертификатов на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="98caf-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="98caf-2384">Применимо, только когда копирование данных выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="98caf-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="98caf-2385">Укажите либо hello `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="98caf-2386">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2386">password</span></span> | <span data-ttu-id="98caf-2387">Пароль, связанный с сертификатом hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="98caf-2388">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2388">No</span></span> |

<span data-ttu-id="98caf-2389">При использовании `certThumbprint` необходимо для проверки подлинности и hello сертификат должен быть установлен в личном хранилище локального компьютера hello hello, служба шлюза toohello разрешение на чтение hello toogrant:</span><span class="sxs-lookup"><span data-stu-id="98caf-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="98caf-2390">Запустите консоль управления (MMC).</span><span class="sxs-lookup"><span data-stu-id="98caf-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="98caf-2391">Добавить hello **сертификаты** этой цели hello оснастки **локального компьютера**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="98caf-2392">Разверните **Сертификаты**, **Личные**, а затем щелкните **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="98caf-2393">Щелкните правой кнопкой мыши hello сертификат из личного хранилища hello и выберите **все задачи**->**управление закрытыми ключами...**</span><span class="sxs-lookup"><span data-stu-id="98caf-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="98caf-2394">На hello **безопасности** добавьте учетную запись пользователя hello, под которой выполняется служба узла шлюза управления данными с сертификатом toohello hello доступ для чтения.</span><span class="sxs-lookup"><span data-stu-id="98caf-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="98caf-2395">**Пример: с использованием клиентского сертификата:** это связанные ссылки на службу данных фабрики tooan локальной HTTP веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="98caf-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="98caf-2396">Она использует сертификат клиента, которая устанавливается на компьютере hello с установлен шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="98caf-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="98caf-2397">Пример: использование сертификата клиента в файле</span><span class="sxs-lookup"><span data-stu-id="98caf-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="98caf-2398">Ссылки на службы связанных данных фабрики tooan локальной HTTP веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="98caf-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="98caf-2399">Он использует файл сертификата клиента на компьютере hello с установлен шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="98caf-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="98caf-2400">Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-2401">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2401">Dataset</span></span>
<span data-ttu-id="98caf-2402">набор данных toodefine HTTP, набор hello **тип** hello набора данных слишком**Http**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2403">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2403">Property</span></span> | <span data-ttu-id="98caf-2404">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2404">Description</span></span> | <span data-ttu-id="98caf-2405">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="98caf-2406">relativeUrl</span></span> | <span data-ttu-id="98caf-2407">Относительный URL-адрес toohello ресурс, содержащий данные hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="98caf-2408">Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны.</span><span class="sxs-lookup"><span data-stu-id="98caf-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="98caf-2409">tooconstruct динамического URL-адреса можно использовать [функции фабрики данных, а системные переменные](data-factory-functions-variables.md), пример: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="98caf-2410">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2410">No</span></span> |
| <span data-ttu-id="98caf-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="98caf-2411">requestMethod</span></span> | <span data-ttu-id="98caf-2412">Метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="98caf-2412">Http method.</span></span> <span data-ttu-id="98caf-2413">Допустимые значения: **GET** или **POST**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="98caf-2414">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-2414">No.</span></span> <span data-ttu-id="98caf-2415">Значение по умолчанию — `GET`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="98caf-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="98caf-2416">additionalHeaders</span></span> | <span data-ttu-id="98caf-2417">Дополнительные заголовки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="98caf-2418">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2418">No</span></span> |
| <span data-ttu-id="98caf-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="98caf-2419">requestBody</span></span> | <span data-ttu-id="98caf-2420">Текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-2420">Body for HTTP request.</span></span> | <span data-ttu-id="98caf-2421">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2421">No</span></span> |
| <span data-ttu-id="98caf-2422">свойства</span><span class="sxs-lookup"><span data-stu-id="98caf-2422">format</span></span> | <span data-ttu-id="98caf-2423">Если требуется toosimply **получения данных hello из конечной точки HTTP-является** без его синтаксического анализа пропустить этот формат параметров.</span><span class="sxs-lookup"><span data-stu-id="98caf-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="98caf-2424">Если требуется ответ hello HTTP tooparse содержимого во время копирования, поддерживаются следующие типы формата hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98caf-2425">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="98caf-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="98caf-2426">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2426">No</span></span> |
| <span data-ttu-id="98caf-2427">compression</span><span class="sxs-lookup"><span data-stu-id="98caf-2427">compression</span></span> | <span data-ttu-id="98caf-2428">Укажите тип hello и уровень сжатия данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="98caf-2429">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98caf-2430">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98caf-2431">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98caf-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98caf-2432">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="98caf-2433">Пример использования hello метод GET (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="98caf-2433">Example: using hello GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="98caf-2434">Пример: с помощью метода POST hello</span><span class="sxs-lookup"><span data-stu-id="98caf-2434">Example: using hello POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="98caf-2435">Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="98caf-2436">Источник HTTP в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2437">При копировании данных из источника HTTP задать hello **тип источника** из hello в действии копирования слишком**HttpSource**и укажите следующие свойства в hello **источника** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-2438">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2438">Property</span></span> | <span data-ttu-id="98caf-2439">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2439">Description</span></span> | <span data-ttu-id="98caf-2440">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="98caf-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="98caf-2441">httpRequestTimeout</span></span> | <span data-ttu-id="98caf-2442">Здравствуйте, время ожидания (TimeSpan) для hello HTTP tooget ответа для запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="98caf-2443">Это tooget hello время ожидания ответа, не hello время ожидания tooread данные ответа.</span><span class="sxs-lookup"><span data-stu-id="98caf-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="98caf-2444">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-2444">No.</span></span> <span data-ttu-id="98caf-2445">Значение по умолчанию  — 00:01:40.</span><span class="sxs-lookup"><span data-stu-id="98caf-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="98caf-2446">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-2447">Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="98caf-2448">OData</span><span class="sxs-lookup"><span data-stu-id="98caf-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-2449">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2449">Linked service</span></span>
<span data-ttu-id="98caf-2450">toodefine OData связанной службы, набор hello **тип** hello связанной службы слишком**OData**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2451">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2451">Property</span></span> | <span data-ttu-id="98caf-2452">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2452">Description</span></span> | <span data-ttu-id="98caf-2453">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2454">url</span><span class="sxs-lookup"><span data-stu-id="98caf-2454">url</span></span> |<span data-ttu-id="98caf-2455">URL-адрес службы OData hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2455">Url of hello OData service.</span></span> |<span data-ttu-id="98caf-2456">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2456">Yes</span></span> |
| <span data-ttu-id="98caf-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2457">authenticationType</span></span> |<span data-ttu-id="98caf-2458">Тип проверки подлинности, используемый источник OData toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="98caf-2459">Возможные значения для облачной службы OData: "Анонимно", "Обычная" и "OAuth" (обратите внимание, что сейчас фабрика данных Azure поддерживает только аутентификацию OAuth на основе Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="98caf-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="98caf-2460">Для локальной службы OData возможными значениями являются "Анонимная", "Обычная" и "Windows".</span><span class="sxs-lookup"><span data-stu-id="98caf-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="98caf-2461">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2461">Yes</span></span> |
| <span data-ttu-id="98caf-2462">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2462">username</span></span> |<span data-ttu-id="98caf-2463">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="98caf-2464">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="98caf-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="98caf-2465">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2465">password</span></span> |<span data-ttu-id="98caf-2466">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-2467">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="98caf-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="98caf-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="98caf-2468">authorizedCredential</span></span> |<span data-ttu-id="98caf-2469">Если вы используете OAuth, нажмите кнопку **авторизовать** приветствия мастера копирования фабрики данных или редактор и введите учетные данные, hello значением этого свойства будет создан.</span><span class="sxs-lookup"><span data-stu-id="98caf-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="98caf-2470">Да (только при использовании аутентификации OAuth)</span><span class="sxs-lookup"><span data-stu-id="98caf-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="98caf-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2471">gatewayName</span></span> |<span data-ttu-id="98caf-2472">Имя шлюза hello, hello служба фабрики данных следует использовать службы OData tooconnect toohello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="98caf-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="98caf-2473">Его необходимо указывать только в том случае, если вы копируете данные из источника в локальной службе OData.</span><span class="sxs-lookup"><span data-stu-id="98caf-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="98caf-2474">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="98caf-2475">Пример: использование обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="98caf-2476">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="98caf-2477">Пример: использование проверки подлинности Windows при получении доступа к локальному источнику OData</span><span class="sxs-lookup"><span data-stu-id="98caf-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="98caf-2478">Пример: использование проверки подлинности OAuth при получении доступа к облачному источнику OData</span><span class="sxs-lookup"><span data-stu-id="98caf-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="98caf-2479">Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="98caf-2480">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2480">Dataset</span></span>
<span data-ttu-id="98caf-2481">toodefine набору данных OData hello набор **тип** hello набора данных слишком**ODataResource**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2482">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2482">Property</span></span> | <span data-ttu-id="98caf-2483">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2483">Description</span></span> | <span data-ttu-id="98caf-2484">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2485">path</span><span class="sxs-lookup"><span data-stu-id="98caf-2485">path</span></span> |<span data-ttu-id="98caf-2486">Путь toohello ресурс OData</span><span class="sxs-lookup"><span data-stu-id="98caf-2486">Path toohello OData resource</span></span> |<span data-ttu-id="98caf-2487">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2488">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="98caf-2489">Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-2490">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2491">При копировании данных из источника OData задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-2492">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2492">Property</span></span> | <span data-ttu-id="98caf-2493">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2493">Description</span></span> | <span data-ttu-id="98caf-2494">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2494">Example</span></span> | <span data-ttu-id="98caf-2495">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2496">query</span><span class="sxs-lookup"><span data-stu-id="98caf-2496">query</span></span> |<span data-ttu-id="98caf-2497">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="98caf-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="98caf-2499">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2500">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="98caf-2501">Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="98caf-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="98caf-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-2503">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2503">Linked service</span></span>
<span data-ttu-id="98caf-2504">toodefine ODBC связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesOdbc**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2505">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2505">Property</span></span> | <span data-ttu-id="98caf-2506">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2506">Description</span></span> | <span data-ttu-id="98caf-2507">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-2508">connectionString</span></span> |<span data-ttu-id="98caf-2509">Hello учетные данные не доступа часть строки подключения hello и необязательный шифрование учетных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="98caf-2510">Примеры в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="98caf-2511">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2511">Yes</span></span> |
| <span data-ttu-id="98caf-2512">credential</span><span class="sxs-lookup"><span data-stu-id="98caf-2512">credential</span></span> |<span data-ttu-id="98caf-2513">учетные данные доступа Hello часть hello строка подключения, указанная в формате значение свойства драйвера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="98caf-2514">Пример: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="98caf-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="98caf-2515">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2515">No</span></span> |
| <span data-ttu-id="98caf-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2516">authenticationType</span></span> |<span data-ttu-id="98caf-2517">Тип проверки подлинности используется хранилище данных tooconnect toohello ODBC.</span><span class="sxs-lookup"><span data-stu-id="98caf-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="98caf-2518">Возможными значениями являются: "Анонимная" и "Обычная".</span><span class="sxs-lookup"><span data-stu-id="98caf-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="98caf-2519">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2519">Yes</span></span> |
| <span data-ttu-id="98caf-2520">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2520">username</span></span> |<span data-ttu-id="98caf-2521">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="98caf-2522">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2522">No</span></span> |
| <span data-ttu-id="98caf-2523">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2523">password</span></span> |<span data-ttu-id="98caf-2524">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-2525">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2525">No</span></span> |
| <span data-ttu-id="98caf-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2526">gatewayName</span></span> |<span data-ttu-id="98caf-2527">Имя шлюза hello, hello служба фабрики данных должна использовать хранилище данных ODBC toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="98caf-2528">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="98caf-2529">Пример: использование обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="98caf-2530">Пример: использование обычной проверки подлинности и шифрования учетных данных</span><span class="sxs-lookup"><span data-stu-id="98caf-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="98caf-2531">Можно зашифровать учетные данные hello, с помощью hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (версии 1.0 Azure PowerShell) командлета или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 или более ранней версии hello Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="98caf-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="98caf-2532">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="98caf-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="98caf-2533">Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-2534">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2534">Dataset</span></span>
<span data-ttu-id="98caf-2535">toodefine набору данных ODBC hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2536">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2536">Property</span></span> | <span data-ttu-id="98caf-2537">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2537">Description</span></span> | <span data-ttu-id="98caf-2538">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-2539">tableName</span></span> |<span data-ttu-id="98caf-2540">Имя таблицы hello в хранилище данных ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="98caf-2541">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="98caf-2542">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-2543">Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-2544">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2545">При копировании данных из хранилища данных ODBC, задайте hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-2546">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2546">Property</span></span> | <span data-ttu-id="98caf-2547">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2547">Description</span></span> | <span data-ttu-id="98caf-2548">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-2548">Allowed values</span></span> | <span data-ttu-id="98caf-2549">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2550">query</span><span class="sxs-lookup"><span data-stu-id="98caf-2550">query</span></span> |<span data-ttu-id="98caf-2551">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-2552">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-2552">SQL query string.</span></span> <span data-ttu-id="98caf-2553">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="98caf-2554">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2555">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="98caf-2556">Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="98caf-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="98caf-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="98caf-2558">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2558">Linked service</span></span>
<span data-ttu-id="98caf-2559">toodefine Salesforce связанной службы, набор hello **тип** hello связанной службы слишком**Salesforce**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2560">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2560">Property</span></span> | <span data-ttu-id="98caf-2561">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2561">Description</span></span> | <span data-ttu-id="98caf-2562">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="98caf-2563">environmentUrl</span></span> | <span data-ttu-id="98caf-2564">Укажите URL-адрес Salesforce экземпляр hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="98caf-2565">— URL-адрес по умолчанию — https://login.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="98caf-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="98caf-2566">-toocopy данных из "песочницы", укажите «https://test.salesforce.com».</span><span class="sxs-lookup"><span data-stu-id="98caf-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="98caf-2567">-задать toocopy данные из пользовательского домена, например, «https://[domain].my.salesforce.com».</span><span class="sxs-lookup"><span data-stu-id="98caf-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="98caf-2568">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2568">No</span></span> |
| <span data-ttu-id="98caf-2569">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2569">username</span></span> |<span data-ttu-id="98caf-2570">Укажите имя пользователя для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="98caf-2571">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2571">Yes</span></span> |
| <span data-ttu-id="98caf-2572">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2572">password</span></span> |<span data-ttu-id="98caf-2573">Укажите пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="98caf-2574">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2574">Yes</span></span> |
| <span data-ttu-id="98caf-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="98caf-2575">securityToken</span></span> |<span data-ttu-id="98caf-2576">Укажите маркер безопасности для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="98caf-2577">В разделе [получение токена безопасности](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) инструкции tooreset/get маркер безопасности.</span><span class="sxs-lookup"><span data-stu-id="98caf-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="98caf-2578">toolearn о маркерах безопасности, см в разделе [безопасности и hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="98caf-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="98caf-2579">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2580">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="98caf-2581">Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-2582">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2582">Dataset</span></span>
<span data-ttu-id="98caf-2583">toodefine набор данных Salesforce hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2584">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2584">Property</span></span> | <span data-ttu-id="98caf-2585">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2585">Description</span></span> | <span data-ttu-id="98caf-2586">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="98caf-2587">tableName</span></span> |<span data-ttu-id="98caf-2588">Имя таблицы hello в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="98caf-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="98caf-2589">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="98caf-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2590">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="98caf-2591">Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="98caf-2592">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2593">При копировании данных из Salesforce задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:</span><span class="sxs-lookup"><span data-stu-id="98caf-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="98caf-2594">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2594">Property</span></span> | <span data-ttu-id="98caf-2595">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2595">Description</span></span> | <span data-ttu-id="98caf-2596">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="98caf-2596">Allowed values</span></span> | <span data-ttu-id="98caf-2597">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98caf-2598">query</span><span class="sxs-lookup"><span data-stu-id="98caf-2598">query</span></span> |<span data-ttu-id="98caf-2599">Используйте данные tooread hello пользовательского запроса.</span><span class="sxs-lookup"><span data-stu-id="98caf-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="98caf-2600">Запрос SQL-92 или запрос, написанный на [объектно-ориентированном языке запросов Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) .</span><span class="sxs-lookup"><span data-stu-id="98caf-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="98caf-2601">Пример: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="98caf-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="98caf-2602">Нет (если hello **tableName** из hello **dataset** указан)</span><span class="sxs-lookup"><span data-stu-id="98caf-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2603">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="98caf-2604">для любого пользовательского объекта требуется Hello «__c» часть hello имя API.</span><span class="sxs-lookup"><span data-stu-id="98caf-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="98caf-2605">Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="98caf-2606">Веб-данные</span><span class="sxs-lookup"><span data-stu-id="98caf-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2607">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2607">Linked service</span></span>
<span data-ttu-id="98caf-2608">веб-узел toodefine связанной службы, набор hello **тип** hello связанной службы слишком**Web**и укажите следующие свойства в hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2609">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2609">Property</span></span> | <span data-ttu-id="98caf-2610">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2610">Description</span></span> | <span data-ttu-id="98caf-2611">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2612">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="98caf-2612">Url</span></span> |<span data-ttu-id="98caf-2613">URL-адрес toohello веб-источнику</span><span class="sxs-lookup"><span data-stu-id="98caf-2613">URL toohello Web source</span></span> |<span data-ttu-id="98caf-2614">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2614">Yes</span></span> |
| <span data-ttu-id="98caf-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="98caf-2615">authenticationType</span></span> |<span data-ttu-id="98caf-2616">Анонимная.</span><span class="sxs-lookup"><span data-stu-id="98caf-2616">Anonymous.</span></span> |<span data-ttu-id="98caf-2617">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="98caf-2618">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="98caf-2619">Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="98caf-2620">Выборка</span><span class="sxs-lookup"><span data-stu-id="98caf-2620">Dataset</span></span>
<span data-ttu-id="98caf-2621">toodefine набора Web hello набор **тип** hello набора данных слишком**таблицы WebTable**и укажите следующие свойства в hello hello **typeProperties** раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="98caf-2622">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2622">Property</span></span> | <span data-ttu-id="98caf-2623">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2623">Description</span></span> | <span data-ttu-id="98caf-2624">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-2625">type</span><span class="sxs-lookup"><span data-stu-id="98caf-2625">type</span></span> |<span data-ttu-id="98caf-2626">Тип набора данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2626">type of hello dataset.</span></span> <span data-ttu-id="98caf-2627">необходимо задать слишком**таблицы WebTable**</span><span class="sxs-lookup"><span data-stu-id="98caf-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="98caf-2628">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2628">Yes</span></span> |
| <span data-ttu-id="98caf-2629">path</span><span class="sxs-lookup"><span data-stu-id="98caf-2629">path</span></span> |<span data-ttu-id="98caf-2630">Относительный URL-адрес ресурса toohello, содержащей таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="98caf-2631">Нет.</span><span class="sxs-lookup"><span data-stu-id="98caf-2631">No.</span></span> <span data-ttu-id="98caf-2632">Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны.</span><span class="sxs-lookup"><span data-stu-id="98caf-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="98caf-2633">index</span><span class="sxs-lookup"><span data-stu-id="98caf-2633">index</span></span> |<span data-ttu-id="98caf-2634">Индекс таблицы hello в ресурсе hello Hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="98caf-2635">В разделе [Get индекс таблицы в HTML-страницу](#get-index-of-a-table-in-an-html-page) раздел для действия toogetting индекса таблицы в HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="98caf-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="98caf-2636">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="98caf-2637">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="98caf-2638">Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="98caf-2639">Веб-источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="98caf-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="98caf-2640">При копировании данных из веб-таблица задать hello **тип источника** из hello в действии копирования слишком**WebSource**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="98caf-2641">В настоящее время, если источник hello в действии копирования имеет тип **WebSource**, дополнительных свойств не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="98caf-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="98caf-2642">Пример</span><span class="sxs-lookup"><span data-stu-id="98caf-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="98caf-2643">Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="98caf-2644">ВЫЧИСЛИТЕЛЬНЫЕ СРЕДЫ</span><span class="sxs-lookup"><span data-stu-id="98caf-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="98caf-2645">Hello следующей таблице перечислены hello вычислительных сред, поддерживаемых фабрику данных и hello преобразования действий, которые можно запустить на них.</span><span class="sxs-lookup"><span data-stu-id="98caf-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="98caf-2646">Щелкните ссылку hello hello вычислений, вы заинтересованы схемы JSON hello toosee для связанной службы toolink его tooa фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="98caf-2647">Вычислительная среда</span><span class="sxs-lookup"><span data-stu-id="98caf-2647">Compute environment</span></span> | <span data-ttu-id="98caf-2648">Действия</span><span class="sxs-lookup"><span data-stu-id="98caf-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="98caf-2649">[Кластер HDInsight по запросу](#on-demand-azure-hdinsight-cluster) или [собственный кластер HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="98caf-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="98caf-2650">[Настраиваемое действие .NET](#net-custom-activity), [действие Hive](#hdinsight-hive-activity), [действие Pig] (#hdinsight-pig-activity), [действие MapReduce](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [действие Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="98caf-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="98caf-2651">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="98caf-2652">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="98caf-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="98caf-2653">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="98caf-2654">[Действие выполнения пакета в службе машинного обучения](#machine-learning-batch-execution-activity), [действие обновления ресурса в службе машинного обучения](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="98caf-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="98caf-2655">Аналитика озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="98caf-2656">Аналитика озера данных U-SQL</span><span class="sxs-lookup"><span data-stu-id="98caf-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="98caf-2657">[База данных Azure SQL](#azure-sql-database-1), [хранилище данных Azure SQL](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="98caf-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="98caf-2658">Хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="98caf-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="98caf-2659">Кластер Azure HDInsight по требованию</span><span class="sxs-lookup"><span data-stu-id="98caf-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="98caf-2660">Hello служба фабрики данных Azure можно автоматически создать на базе Windows или Linux данных по запросу для tooprocess кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="98caf-2661">кластер Hello создается в одном регионе с учетной записью хранения hello (свойство linkedServiceName в hello JSON), связанные с кластером hello hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="98caf-2662">Можно выполнить после преобразования действий на эта связанная служба hello: [настраиваемых действий .NET](#net-custom-activity), [Hive действия](#hdinsight-hive-activity), [Действие Pig] (#hdinsight pig операции, [действия MapReduce ](#hdinsight-mapreduce-activity), [Действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [усилить действия](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="98caf-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2663">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2663">Linked service</span></span> 
<span data-ttu-id="98caf-2664">Привет, в следующей таблице приводится описание свойств hello, используемых в определении Azure JSON hello по требованию связанной службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="98caf-2665">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2665">Property</span></span> | <span data-ttu-id="98caf-2666">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2666">Description</span></span> | <span data-ttu-id="98caf-2667">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2668">type</span><span class="sxs-lookup"><span data-stu-id="98caf-2668">type</span></span> |<span data-ttu-id="98caf-2669">свойство типа Hello должно быть установлено слишком**HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="98caf-2670">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2670">Yes</span></span> |
| <span data-ttu-id="98caf-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="98caf-2671">clusterSize</span></span> |<span data-ttu-id="98caf-2672">Количество узлов данных рабочего процесса или в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="98caf-2673">Создание кластера HDInsight Hello с 2 головного узла вместе с hello число рабочих узлов, которые указаны для этого свойства.</span><span class="sxs-lookup"><span data-stu-id="98caf-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="98caf-2674">Hello узлы имеют размер Standard_D3, который имеет 4 ядра, поэтому 4 рабочий узел кластера будет 24 ядра (4\*4 = 16 ядер для рабочих узлов, плюс 2\*4 = 8 ядер для головного узла).</span><span class="sxs-lookup"><span data-stu-id="98caf-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="98caf-2675">В разделе [кластеров под управлением Linux, создать Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) для получения сведений об hello Standard_D3 уровня.</span><span class="sxs-lookup"><span data-stu-id="98caf-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="98caf-2676">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2676">Yes</span></span> |
| <span data-ttu-id="98caf-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="98caf-2677">timetolive</span></span> |<span data-ttu-id="98caf-2678">Hello допустимое время простоя для кластера HDInsight по требованию hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="98caf-2679">Указывает, как долго кластер HDInsight по требованию hello остается активным после завершения действий при наличии других активных заданий в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="98caf-2680">Например, если при выполнении действия занимает 6 минут и timetolive установлен too5 минут, hello кластер остается активным на 5 минут после hello 6 минут обработки при выполнении действия hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="98caf-2681">Если при выполнении другого действия выполняется с окном приветствия 6 минут, он обрабатывается hello одного кластера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="98caf-2682">Создание кластера HDInsight по требованию является ресурсоемкой операцией (может потребоваться некоторое время), поэтому используйте этот параметр как необходимые tooimprove производительности фабрики данных, используя кластер HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="98caf-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="98caf-2683">Если задать значение too0 timetolive hello кластера удаляется сразу hello выполняться действие обработанном.</span><span class="sxs-lookup"><span data-stu-id="98caf-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="98caf-2684">На hello другой стороны, если задано большое значение, hello кластера может оставаться простоя, без необходимости приведет к высокой затраты.</span><span class="sxs-lookup"><span data-stu-id="98caf-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="98caf-2685">Таким образом важно задать соответствующее значение hello зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="98caf-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="98caf-2686">Можно совместно использовать несколько конвейеров hello же экземпляр кластера HDInsight по требованию hello, если соответствующим образом задано значение свойства timetolive hello</span><span class="sxs-lookup"><span data-stu-id="98caf-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="98caf-2687">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2687">Yes</span></span> |
| <span data-ttu-id="98caf-2688">версия</span><span class="sxs-lookup"><span data-stu-id="98caf-2688">version</span></span> |<span data-ttu-id="98caf-2689">Версия кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="98caf-2690">Подробные сведения см. в статье [Версии HDInsight, поддерживаемые в фабрике данных Azure](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="98caf-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="98caf-2691">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2691">No</span></span> |
| <span data-ttu-id="98caf-2692">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-2692">linkedServiceName</span></span> |<span data-ttu-id="98caf-2693">Связанная служба toobe, используемой кластером по требованию hello для хранения и обработки данных хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="98caf-2694">В настоящее время не удается создать кластер HDInsight по требованию, использующий хранилища Озера данных Azure в качестве хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="98caf-2695">Результирующие данные hello toostore обработки в хранилище Озера данных Azure HDInsight, используйте действие копирования toocopy hello данных из хранилища больших двоичных объектов hello toohello хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="98caf-2696">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2696">Yes</span></span> |
| <span data-ttu-id="98caf-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="98caf-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="98caf-2698">Указывает, что дополнительные учетные записи хранения для hello HDInsight связанной службы, чтобы служба фабрики данных hello зарегистрировать их от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="98caf-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="98caf-2699">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2699">No</span></span> |
| <span data-ttu-id="98caf-2700">osType</span><span class="sxs-lookup"><span data-stu-id="98caf-2700">osType</span></span> |<span data-ttu-id="98caf-2701">Тип операционной системы.</span><span class="sxs-lookup"><span data-stu-id="98caf-2701">Type of operating system.</span></span> <span data-ttu-id="98caf-2702">Допустимые значения: Windows (по умолчанию) и Linux.</span><span class="sxs-lookup"><span data-stu-id="98caf-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="98caf-2703">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2703">No</span></span> |
| <span data-ttu-id="98caf-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="98caf-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="98caf-2705">Имя Hello SQL Azure связанные службы этой базы данных HCatalog toohello точки.</span><span class="sxs-lookup"><span data-stu-id="98caf-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="98caf-2706">кластер HDInsight по требованию Hello создается с помощью базы данных Azure SQL hello как метахранилище hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="98caf-2707">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="98caf-2708">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2708">JSON example</span></span>
<span data-ttu-id="98caf-2709">Привет, следуя JSON определяет под управлением Linux по требованию связанной службы HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="98caf-2710">Hello служба фабрики данных автоматически создает **под управлением Linux** кластера HDInsight при обработке срез данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="98caf-2711">Дополнительные сведения см. в статье [Вычислительные среды, поддерживаемые фабрикой данных Azure](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="98caf-2712">Имеющийся кластер Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="98caf-2713">Можно создать кластер HDInsight tooregister службы Azure HDInsight связанные с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="98caf-2714">Можно запустить hello Далее эта связанная служба действия преобразования данных: [настраиваемых действий .NET](#net-custom-activity), [Hive действия](#hdinsight-hive-activity), [Действие Pig] (#hdinsight pig операции, [MapReduce Действие](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [усилить действия](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="98caf-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2715">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2715">Linked service</span></span>
<span data-ttu-id="98caf-2716">Привет, в следующей таблице приводится описание свойств hello, используемых в определении Azure JSON hello связанная служба Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="98caf-2717">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2717">Property</span></span> | <span data-ttu-id="98caf-2718">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2718">Description</span></span> | <span data-ttu-id="98caf-2719">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2720">type</span><span class="sxs-lookup"><span data-stu-id="98caf-2720">type</span></span> |<span data-ttu-id="98caf-2721">свойство типа Hello должно быть установлено слишком**HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="98caf-2722">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2722">Yes</span></span> |
| <span data-ttu-id="98caf-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="98caf-2723">clusterUri</span></span> |<span data-ttu-id="98caf-2724">Здравствуйте, URI кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="98caf-2725">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2725">Yes</span></span> |
| <span data-ttu-id="98caf-2726">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2726">username</span></span> |<span data-ttu-id="98caf-2727">Укажите имя hello toobe hello пользователя используется существующий кластер HDInsight tooconnect tooan.</span><span class="sxs-lookup"><span data-stu-id="98caf-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="98caf-2728">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2728">Yes</span></span> |
| <span data-ttu-id="98caf-2729">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2729">password</span></span> |<span data-ttu-id="98caf-2730">Укажите пароль для учетной записи пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="98caf-2731">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2731">Yes</span></span> |
| <span data-ttu-id="98caf-2732">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-2732">linkedServiceName</span></span> | <span data-ttu-id="98caf-2733">Имя связанной службой хранилища Azure, ссылающийся на хранилище больших двоичных объектов toohello hello используется hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="98caf-2734">В настоящее время для этого свойства невозможно указать связанную службу Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98caf-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="98caf-2735">Может доступа к данным в hello хранилища Озера данных Azure из скриптов Hive и Pig Если кластера HDInsight hello toohello доступа хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="98caf-2736">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2736">Yes</span></span> |

<span data-ttu-id="98caf-2737">Список поддерживаемых версий кластеров HDInsight см. в статье [Поддерживаемые версии HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="98caf-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="98caf-2738">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="98caf-2739">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2739">Azure Batch</span></span>
<span data-ttu-id="98caf-2740">Можно создать пул пакета виртуальных машин (ВМ) tooregister службы связанной пакетной службы Azure с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="98caf-2741">Пользовательские действия .NET можно выполнять с помощью пакетной службы Azure или службы Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="98caf-2742">В этой связанной службе можно запустить [настраиваемое действие .NET](#net-custom-activity).</span><span class="sxs-lookup"><span data-stu-id="98caf-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2743">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2743">Linked service</span></span>
<span data-ttu-id="98caf-2744">Hello в следующей таблице приводится описание свойств hello, используемых в определении hello Azure JSON связанной пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="98caf-2745">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2745">Property</span></span> | <span data-ttu-id="98caf-2746">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2746">Description</span></span> | <span data-ttu-id="98caf-2747">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2748">type</span><span class="sxs-lookup"><span data-stu-id="98caf-2748">type</span></span> |<span data-ttu-id="98caf-2749">свойство типа Hello должно быть установлено слишком**AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="98caf-2750">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2750">Yes</span></span> |
| <span data-ttu-id="98caf-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="98caf-2751">accountName</span></span> |<span data-ttu-id="98caf-2752">Имя учетной записи пакетной службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="98caf-2753">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2753">Yes</span></span> |
| <span data-ttu-id="98caf-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="98caf-2754">accessKey</span></span> |<span data-ttu-id="98caf-2755">Ключ доступа для учетной записи пакетной службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="98caf-2756">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2756">Yes</span></span> |
| <span data-ttu-id="98caf-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="98caf-2757">poolName</span></span> |<span data-ttu-id="98caf-2758">Имя пула hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="98caf-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="98caf-2759">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2759">Yes</span></span> |
| <span data-ttu-id="98caf-2760">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="98caf-2760">linkedServiceName</span></span> |<span data-ttu-id="98caf-2761">Имя связанной службой хранилища Azure связанные с этой связанной пакетной службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="98caf-2762">Эта связанная служба используется для промежуточных файлов необходимые действия toorun hello и хранения журналов выполнения действия hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="98caf-2763">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="98caf-2764">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="98caf-2765">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2765">Azure Machine Learning</span></span>
<span data-ttu-id="98caf-2766">Создание службы машинного обучения Azure связаны tooregister конечной точки с фабрикой данных оценки пакета машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="98caf-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="98caf-2767">В этой связанной службе можно выполнять два действия преобразования данных: [действие выполнения пакета в службе машинного обучения](#machine-learning-batch-execution-activity), [действие обновления ресурса службы машинного обучения](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="98caf-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2768">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2768">Linked service</span></span>
<span data-ttu-id="98caf-2769">Привет, в следующей таблице приводится описание свойств hello, используемых в определении Azure JSON hello Azure связанной службы машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="98caf-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="98caf-2770">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2770">Property</span></span> | <span data-ttu-id="98caf-2771">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2771">Description</span></span> | <span data-ttu-id="98caf-2772">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2773">Тип</span><span class="sxs-lookup"><span data-stu-id="98caf-2773">Type</span></span> |<span data-ttu-id="98caf-2774">свойство типа Hello должно быть присвоено: **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="98caf-2775">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2775">Yes</span></span> |
| <span data-ttu-id="98caf-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="98caf-2776">mlEndpoint</span></span> |<span data-ttu-id="98caf-2777">URL-адрес оценки пакета Hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="98caf-2778">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2778">Yes</span></span> |
| <span data-ttu-id="98caf-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="98caf-2779">apiKey</span></span> |<span data-ttu-id="98caf-2780">Hello опубликованы API модели рабочей области.</span><span class="sxs-lookup"><span data-stu-id="98caf-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="98caf-2781">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="98caf-2782">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="98caf-2783">Аналитика озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="98caf-2784">Вы создаете **аналитики Озера данных Azure** связанные toolink служба фабрики данных Azure compute Служба аналитики Озера данных Azure tooan перед использованием hello [действия U-SQL аналитики Озера данных](data-factory-usql-activity.md) в конвейере .</span><span class="sxs-lookup"><span data-stu-id="98caf-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="98caf-2785">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2785">Linked service</span></span>

<span data-ttu-id="98caf-2786">Hello в следующей таблице приводится описание свойств hello, используемых в определении JSON hello службы связаны аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="98caf-2787">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2787">Property</span></span> | <span data-ttu-id="98caf-2788">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2788">Description</span></span> | <span data-ttu-id="98caf-2789">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2790">Тип</span><span class="sxs-lookup"><span data-stu-id="98caf-2790">Type</span></span> |<span data-ttu-id="98caf-2791">свойство типа Hello должно быть присвоено: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="98caf-2792">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2792">Yes</span></span> |
| <span data-ttu-id="98caf-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="98caf-2793">accountName</span></span> |<span data-ttu-id="98caf-2794">Имя учетной записи аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="98caf-2795">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2795">Yes</span></span> |
| <span data-ttu-id="98caf-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="98caf-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="98caf-2797">Универсальный код ресурса (URI) аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="98caf-2798">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2798">No</span></span> |
| <span data-ttu-id="98caf-2799">authorization</span><span class="sxs-lookup"><span data-stu-id="98caf-2799">authorization</span></span> |<span data-ttu-id="98caf-2800">Код авторизации будет извлечен автоматически после щелкнув **авторизовать** кнопку в hello редактор фабрики данных и завершение входа OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="98caf-2801">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2801">Yes</span></span> |
| <span data-ttu-id="98caf-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="98caf-2802">subscriptionId</span></span> |<span data-ttu-id="98caf-2803">Идентификатор подписки Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2803">Azure subscription id</span></span> |<span data-ttu-id="98caf-2804">Нет (если не указан, подписка hello используется фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="98caf-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="98caf-2805">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="98caf-2805">resourceGroupName</span></span> |<span data-ttu-id="98caf-2806">Имя группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2806">Azure resource group name</span></span> |<span data-ttu-id="98caf-2807">Нет (если не указан, группа ресурсов для hello используется фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="98caf-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="98caf-2808">sessionid</span><span class="sxs-lookup"><span data-stu-id="98caf-2808">sessionId</span></span> |<span data-ttu-id="98caf-2809">Идентификатор сеанса из сеанса авторизации OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="98caf-2810">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="98caf-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="98caf-2811">При использовании hello редактор фабрики данных, этот идентификатор создан автоматически.</span><span class="sxs-lookup"><span data-stu-id="98caf-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="98caf-2812">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="98caf-2813">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2813">JSON example</span></span>
<span data-ttu-id="98caf-2814">Следующий пример Hello предоставляет определение JSON для связанной аналитики Озера данных Azure службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="98caf-2815">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2815">Azure SQL Database</span></span>
<span data-ttu-id="98caf-2816">Создание связанной службой Azure SQL и использовать ее с hello [действия хранимой процедуры](#stored-procedure-activity) tooinvoke хранимой процедуры из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2817">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2817">Linked service</span></span>
<span data-ttu-id="98caf-2818">toodefine базы данных SQL Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDatabase**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2819">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2819">Property</span></span> | <span data-ttu-id="98caf-2820">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2820">Description</span></span> | <span data-ttu-id="98caf-2821">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-2822">connectionString</span></span> |<span data-ttu-id="98caf-2823">Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных SQL Azure toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="98caf-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="98caf-2824">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="98caf-2825">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="98caf-2826">Дополнительную информацию см. в статье о [связанной службе SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="98caf-2827">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="98caf-2828">Создание службы связаны хранилища данных SQL Azure и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2829">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2829">Linked service</span></span>
<span data-ttu-id="98caf-2830">Хранилище данных SQL Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDW**и укажите следующие свойства в hello **typeProperties**раздела:</span><span class="sxs-lookup"><span data-stu-id="98caf-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="98caf-2831">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2831">Property</span></span> | <span data-ttu-id="98caf-2832">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2832">Description</span></span> | <span data-ttu-id="98caf-2833">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-2834">connectionString</span></span> |<span data-ttu-id="98caf-2835">Укажите сведения, необходимые для свойства connectionString hello tooconnect toohello хранилище данных SQL Azure экземпляра.</span><span class="sxs-lookup"><span data-stu-id="98caf-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="98caf-2836">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="98caf-2837">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="98caf-2838">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="98caf-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="98caf-2839">SQL Server</span></span> 
<span data-ttu-id="98caf-2840">Создание связанной службы SQL Server и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="98caf-2841">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="98caf-2841">Linked service</span></span>
<span data-ttu-id="98caf-2842">Создание связанной службы типа **OnPremisesSqlServer** toolink фабрикой данных базы данных tooa в локальной среде SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="98caf-2843">Привет, в следующей таблице приводится описание JSON элементов определенного tooon локальной связанной службы SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="98caf-2844">Привет, в следующей таблице приводится описание tooSQL определенные элементы JSON службы связанного сервера.</span><span class="sxs-lookup"><span data-stu-id="98caf-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="98caf-2845">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2845">Property</span></span> | <span data-ttu-id="98caf-2846">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2846">Description</span></span> | <span data-ttu-id="98caf-2847">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2848">type</span><span class="sxs-lookup"><span data-stu-id="98caf-2848">type</span></span> |<span data-ttu-id="98caf-2849">свойство типа Hello должно быть присвоено: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="98caf-2850">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2850">Yes</span></span> |
| <span data-ttu-id="98caf-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="98caf-2851">connectionString</span></span> |<span data-ttu-id="98caf-2852">Укажите сведения connectionString, необходимые tooconnect toohello локальной SQL Server базы данных с помощью проверки подлинности Windows или проверка подлинности SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="98caf-2853">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2853">Yes</span></span> |
| <span data-ttu-id="98caf-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="98caf-2854">gatewayName</span></span> |<span data-ttu-id="98caf-2855">Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="98caf-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="98caf-2856">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2856">Yes</span></span> |
| <span data-ttu-id="98caf-2857">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="98caf-2857">username</span></span> |<span data-ttu-id="98caf-2858">При использовании проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="98caf-2859">Например, **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="98caf-2860">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2860">No</span></span> |
| <span data-ttu-id="98caf-2861">пароль</span><span class="sxs-lookup"><span data-stu-id="98caf-2861">password</span></span> |<span data-ttu-id="98caf-2862">Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="98caf-2863">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2863">No</span></span> |

<span data-ttu-id="98caf-2864">Вы можете зашифровать учетные данные с помощью hello **New AzureRmDataFactoryEncryptValue** командлета и использовать их в строке подключения hello, как показано в следующий пример hello (**EncryptedCredential** свойство):</span><span class="sxs-lookup"><span data-stu-id="98caf-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="98caf-2865">Пример: JSON для использования проверки подлинности SQL</span><span class="sxs-lookup"><span data-stu-id="98caf-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="98caf-2866">Пример: JSON для использования проверки подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="98caf-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="98caf-2867">Если указаны имя пользователя и пароль, шлюз использует их tooimpersonate hello базы данных SQL Server в локальной toohello в tooconnect учетную запись указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="98caf-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="98caf-2868">В противном случае шлюз подключается toohello SQL Server непосредственно с контекстом безопасности hello шлюза (его учетная запись для запуска).</span><span class="sxs-lookup"><span data-stu-id="98caf-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="98caf-2869">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98caf-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="98caf-2870">Действия преобразования данных</span><span class="sxs-lookup"><span data-stu-id="98caf-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="98caf-2871">Действие</span><span class="sxs-lookup"><span data-stu-id="98caf-2871">Activity</span></span> | <span data-ttu-id="98caf-2872">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="98caf-2873">Действие Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="98caf-2874">Hello действие Hive в HDInsight из конвейера фабрики данных выполняет запросы Hive самостоятельно или кластера HDInsight под управлением Windows и Linux по требованию.</span><span class="sxs-lookup"><span data-stu-id="98caf-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="98caf-2875">Действие Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="98caf-2876">Hello действие Pig с HDInsight из конвейера фабрики данных выполняет собственную запросов Pig или кластера HDInsight под управлением Windows и Linux по требованию.</span><span class="sxs-lookup"><span data-stu-id="98caf-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="98caf-2877">Действие MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="98caf-2878">Hello действие MapReduce в HDInsight из конвейера фабрики данных выполняет программ MapReduce самостоятельно или кластера HDInsight под управлением Windows и Linux по требованию.</span><span class="sxs-lookup"><span data-stu-id="98caf-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="98caf-2879">Действие потоковой передачи HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="98caf-2880">Hello действие потоковой передачи HDInsight из конвейера фабрики данных выполняет программ потоковой передачи Hadoop на локальном или кластера HDInsight под управлением Windows и Linux по требованию.</span><span class="sxs-lookup"><span data-stu-id="98caf-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="98caf-2881">Действие HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="98caf-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="98caf-2882">Hello действия HDInsight Spark в конвейере фабрики данных выполняет программы Spark в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="98caf-2883">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="98caf-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="98caf-2884">Azure позволяет фабрики данных, вы tooeasily создавать конвейеры, использующих опубликованные машинного обучения Azure веб-службы для прогнозирования.</span><span class="sxs-lookup"><span data-stu-id="98caf-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="98caf-2885">С помощью hello действие выполнения пакета в конвейере фабрики данных Azure, можно вызвать прогнозы машинного обучения веб-службы toomake на hello данных в пакете.</span><span class="sxs-lookup"><span data-stu-id="98caf-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="98caf-2886">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="98caf-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="98caf-2887">Со временем hello прогнозных моделей в hello машинного обучения, оценки экспериментов требуется toobe повторное обучение с помощью нового входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="98caf-2888">После завершения переподготовки, вы хотите tooupdate hello оценки веб-службы с hello повторное Обучение модели машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="98caf-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="98caf-2889">Hello действия ресурса обновления tooupdate hello веб-службы можно использовать с hello вновь обучения модели.</span><span class="sxs-lookup"><span data-stu-id="98caf-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="98caf-2890">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="98caf-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="98caf-2891">Действие hello хранимую процедуру можно использовать в tooinvoke конвейера фабрики данных хранимой процедуры в одном hello, следуя хранилищ данных: базы данных SQL Azure, хранилище данных SQL Azure, база данных SQL Server в вашей организации или Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="98caf-2892">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="98caf-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="98caf-2893">Действие U-SQL Data Lake Analytics запускает сценарий U-SQL для кластера Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="98caf-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="98caf-2894">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="98caf-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="98caf-2895">Если требуются данные tootransform способом, не поддерживаемый фабрики данных, можно создать пользовательское действие с свою собственную логику для обработки данных и использовать hello действия в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="98caf-2896">Вы можете настроить toorun .NET действие hello для пользовательских с помощью пакетной службы Azure или кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="98caf-2897">Действие Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="98caf-2898">Можно указать следующие свойства в определении JSON действия Hive hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="98caf-2899">свойство типа Hello для действия "hello" должно быть: **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="98caf-2900">Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-2901">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightHive действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="98caf-2902">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2902">Property</span></span> | <span data-ttu-id="98caf-2903">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2903">Description</span></span> | <span data-ttu-id="98caf-2904">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2905">script</span><span class="sxs-lookup"><span data-stu-id="98caf-2905">script</span></span> |<span data-ttu-id="98caf-2906">Укажите встроенного скрипта Hive hello</span><span class="sxs-lookup"><span data-stu-id="98caf-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="98caf-2907">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2907">No</span></span> |
| <span data-ttu-id="98caf-2908">script path</span><span class="sxs-lookup"><span data-stu-id="98caf-2908">script path</span></span> |<span data-ttu-id="98caf-2909">Хранилище hello Hive скрипт в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="98caf-2910">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="98caf-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="98caf-2911">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="98caf-2911">Both cannot be used together.</span></span> <span data-ttu-id="98caf-2912">Имя файла Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="98caf-2913">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2913">No</span></span> |
| <span data-ttu-id="98caf-2914">defines</span><span class="sxs-lookup"><span data-stu-id="98caf-2914">defines</span></span> |<span data-ttu-id="98caf-2915">Укажите параметры как пары "ключ значение" для ссылки на куст скрипте hello «hiveconf»</span><span class="sxs-lookup"><span data-stu-id="98caf-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="98caf-2916">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2916">No</span></span> |

<span data-ttu-id="98caf-2917">Эти свойства типа, определенного toohello действие Hive.</span><span class="sxs-lookup"><span data-stu-id="98caf-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="98caf-2918">Другие свойства (за пределами hello раздел typeProperties) поддерживаются для всех действий.</span><span class="sxs-lookup"><span data-stu-id="98caf-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="98caf-2919">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2919">JSON example</span></span>
<span data-ttu-id="98caf-2920">Привет, следуя JSON определяет действие Hive в HDInsight в конвейере.</span><span class="sxs-lookup"><span data-stu-id="98caf-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
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

<span data-ttu-id="98caf-2921">Дополнительные сведения см. в статье о [действии Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="98caf-2922">Действие Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="98caf-2923">Можно указать следующие свойства в определении JSON действия Pig hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="98caf-2924">свойство типа Hello для действия "hello" должно быть: **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="98caf-2925">Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-2926">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightPig действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="98caf-2927">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2927">Property</span></span> | <span data-ttu-id="98caf-2928">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2928">Description</span></span> | <span data-ttu-id="98caf-2929">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2930">script</span><span class="sxs-lookup"><span data-stu-id="98caf-2930">script</span></span> |<span data-ttu-id="98caf-2931">Укажите встроенного скрипта Pig hello</span><span class="sxs-lookup"><span data-stu-id="98caf-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="98caf-2932">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2932">No</span></span> |
| <span data-ttu-id="98caf-2933">script path</span><span class="sxs-lookup"><span data-stu-id="98caf-2933">script path</span></span> |<span data-ttu-id="98caf-2934">Хранить сценарий Pig hello в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="98caf-2935">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="98caf-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="98caf-2936">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="98caf-2936">Both cannot be used together.</span></span> <span data-ttu-id="98caf-2937">Имя файла Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="98caf-2938">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2938">No</span></span> |
| <span data-ttu-id="98caf-2939">defines</span><span class="sxs-lookup"><span data-stu-id="98caf-2939">defines</span></span> |<span data-ttu-id="98caf-2940">Укажите параметры как пары "ключ значение" для ссылки в пределах hello сценарий Pig</span><span class="sxs-lookup"><span data-stu-id="98caf-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="98caf-2941">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2941">No</span></span> |

<span data-ttu-id="98caf-2942">Эти свойства типа, определенного toohello действие Pig.</span><span class="sxs-lookup"><span data-stu-id="98caf-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="98caf-2943">Другие свойства (за пределами hello раздел typeProperties) поддерживаются для всех действий.</span><span class="sxs-lookup"><span data-stu-id="98caf-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="98caf-2944">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2944">JSON example</span></span>

```json
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

<span data-ttu-id="98caf-2945">Дополнительные сведения см. в статье о [действии Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="98caf-2946">Действие MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="98caf-2947">Можно указать следующие свойства в определении JSON действия MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="98caf-2948">свойство типа Hello для действия "hello" должно быть: **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="98caf-2949">Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-2950">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightMapReduce действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="98caf-2951">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2951">Property</span></span> | <span data-ttu-id="98caf-2952">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2952">Description</span></span> | <span data-ttu-id="98caf-2953">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="98caf-2954">jarLinkedService</span></span> | <span data-ttu-id="98caf-2955">Имя hello связанной службы для hello хранилища Azure, содержащую hello JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="98caf-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="98caf-2956">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2956">Yes</span></span> |
| <span data-ttu-id="98caf-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="98caf-2957">jarFilePath</span></span> | <span data-ttu-id="98caf-2958">Путь к файлу toohello JAR в hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="98caf-2959">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2959">Yes</span></span> | 
| <span data-ttu-id="98caf-2960">className</span><span class="sxs-lookup"><span data-stu-id="98caf-2960">className</span></span> | <span data-ttu-id="98caf-2961">Имя основного класса hello в hello JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="98caf-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="98caf-2962">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-2962">Yes</span></span> | 
| <span data-ttu-id="98caf-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="98caf-2963">arguments</span></span> | <span data-ttu-id="98caf-2964">Список разделенных запятыми аргументов для программы MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="98caf-2965">Во время выполнения, появится несколько дополнительных аргументов (например: mapreduce.job.tags) на основе инфраструктуры MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="98caf-2966">toodifferentiate аргументов с аргументами MapReduce hello, рассмотрите использование параметра и значение в качестве аргументов, как показано в следующий пример hello (- s,--входных данных, — т. д., выходные данные будут сразу следуют значениями параметров)</span><span class="sxs-lookup"><span data-stu-id="98caf-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="98caf-2967">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="98caf-2968">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
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
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="98caf-2969">Дополнительные сведения см. в статье о [действии MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="98caf-2970">Действие потоковой передачи HDInsight</span><span class="sxs-lookup"><span data-stu-id="98caf-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="98caf-2971">Можно указать следующие свойства в определении JSON действия потоковой передачи Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="98caf-2972">свойство типа Hello для действия "hello" должно быть: **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="98caf-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="98caf-2973">Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-2974">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightStreaming действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="98caf-2975">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-2975">Property</span></span> | <span data-ttu-id="98caf-2976">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="98caf-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="98caf-2977">mapper</span></span> | <span data-ttu-id="98caf-2978">Имя исполняемого файла модуля сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="98caf-2979">В примере hello cat.exe является исполняемого файла модуля сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="98caf-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="98caf-2980">reducer</span></span> | <span data-ttu-id="98caf-2981">Имя исполняемого файла редуктора hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="98caf-2982">В примере hello wc.exe — исполняемого файла редуктора hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="98caf-2983">input</span><span class="sxs-lookup"><span data-stu-id="98caf-2983">input</span></span> | <span data-ttu-id="98caf-2984">Входной файл (в том числе расположение) для сопоставления hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="98caf-2985">В примере hello: «wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt»: adfsample — контейнер больших двоичных объектов hello, пример/data/Gutenberg — папка hello и davinci.txt — hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="98caf-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="98caf-2986">output</span><span class="sxs-lookup"><span data-stu-id="98caf-2986">output</span></span> | <span data-ttu-id="98caf-2987">Выходной файл (в том числе расположение) для hello редуктора.</span><span class="sxs-lookup"><span data-stu-id="98caf-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="98caf-2988">выходные данные задания потоковой передачи Hadoop hello Hello записывается toohello расположение, заданное для этого свойства.</span><span class="sxs-lookup"><span data-stu-id="98caf-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="98caf-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="98caf-2989">filePaths</span></span> | <span data-ttu-id="98caf-2990">Пути для исполняемых файлов сопоставления и редуктора hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="98caf-2991">В примере hello: «adfsample/example/apps/wc.exe» adfsample — hello контейнер больших двоичных объектов, example/apps — папка hello и wc.exe — hello исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="98caf-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="98caf-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="98caf-2992">fileLinkedService</span></span> | <span data-ttu-id="98caf-2993">Связанная служба, которая представляет hello хранилища Azure, содержащей hello файлы, указанные в разделе filePaths hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="98caf-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="98caf-2994">arguments</span></span> | <span data-ttu-id="98caf-2995">Список разделенных запятыми аргументов для программы MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="98caf-2996">Во время выполнения, появится несколько дополнительных аргументов (например: mapreduce.job.tags) на основе инфраструктуры MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="98caf-2997">toodifferentiate аргументов с аргументами MapReduce hello, рассмотрите использование параметра и значение в качестве аргументов, как показано в следующий пример hello (- s,--входных данных, — т. д., выходные данные будут сразу следуют значениями параметров)</span><span class="sxs-lookup"><span data-stu-id="98caf-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="98caf-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="98caf-2998">getDebugInfo</span></span> | <span data-ttu-id="98caf-2999">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="98caf-2999">An optional element.</span></span> <span data-ttu-id="98caf-3000">Если он имеет значение tooFailure, hello журналы будут загружены только при сбое.</span><span class="sxs-lookup"><span data-stu-id="98caf-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="98caf-3001">Если он имеет значение tooAll, журналы, загружаются всегда независимо от состояния выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="98caf-3002">Необходимо указать выходной набор данных для hello действие потоковой передачи Hadoop для hello **выводит** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="98caf-3003">Этот набор данных может быть просто пустой набор данных, необходимые toodrive hello конвейера расписание (каждый час, день, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="98caf-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="98caf-3004">Если действие hello не принимает входных данных, можно пропустить, указав входного набора данных для действия "hello" для hello **входов** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="98caf-3005">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3005">JSON example</span></span>

```json
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
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
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
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="98caf-3006">Дополнительные сведения см. в статье о [действии потоковой передачи Hadoop](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="98caf-3007">Действие HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="98caf-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="98caf-3008">Можно указать следующие свойства в определении JSON действия Spark hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="98caf-3009">свойство типа Hello для действия "hello" должно быть: **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="98caf-3010">Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-3011">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightSpark действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="98caf-3012">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-3012">Property</span></span> | <span data-ttu-id="98caf-3013">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-3013">Description</span></span> | <span data-ttu-id="98caf-3014">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="98caf-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="98caf-3015">rootPath</span></span> | <span data-ttu-id="98caf-3016">контейнер больших двоичных объектов Azure Hello и папку, содержащую файл Spark hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="98caf-3017">Имя файла Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="98caf-3018">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3018">Yes</span></span> |
| <span data-ttu-id="98caf-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="98caf-3019">entryFilePath</span></span> | <span data-ttu-id="98caf-3020">Относительный путь toohello корневую папку hello пакет кода Spark.</span><span class="sxs-lookup"><span data-stu-id="98caf-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="98caf-3021">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3021">Yes</span></span> |
| <span data-ttu-id="98caf-3022">className</span><span class="sxs-lookup"><span data-stu-id="98caf-3022">className</span></span> | <span data-ttu-id="98caf-3023">Основной класс Java или Spark приложения.</span><span class="sxs-lookup"><span data-stu-id="98caf-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="98caf-3024">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3024">No</span></span> | 
| <span data-ttu-id="98caf-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="98caf-3025">arguments</span></span> | <span data-ttu-id="98caf-3026">Список аргументов командной строки toohello Spark программы.</span><span class="sxs-lookup"><span data-stu-id="98caf-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="98caf-3027">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3027">No</span></span> | 
| <span data-ttu-id="98caf-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="98caf-3028">proxyUser</span></span> | <span data-ttu-id="98caf-3029">Hello учетной записи пользователя tooimpersonate tooexecute hello Spark программы</span><span class="sxs-lookup"><span data-stu-id="98caf-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="98caf-3030">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3030">No</span></span> | 
| <span data-ttu-id="98caf-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="98caf-3031">sparkConfig</span></span> | <span data-ttu-id="98caf-3032">Свойства конфигурации Spark.</span><span class="sxs-lookup"><span data-stu-id="98caf-3032">Spark configuration properties.</span></span> | <span data-ttu-id="98caf-3033">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3033">No</span></span> | 
| <span data-ttu-id="98caf-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="98caf-3034">getDebugInfo</span></span> | <span data-ttu-id="98caf-3035">Указывает при файлов журнала Spark hello скопированный toohello хранилища Azure в кластере HDInsight (или) заданные sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="98caf-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="98caf-3036">Допустимые значения: None, Always или Failure.</span><span class="sxs-lookup"><span data-stu-id="98caf-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="98caf-3037">Значение по умолчанию: None.</span><span class="sxs-lookup"><span data-stu-id="98caf-3037">Default value: None.</span></span> | <span data-ttu-id="98caf-3038">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3038">No</span></span> | 
| <span data-ttu-id="98caf-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="98caf-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="98caf-3040">Hello связанной службой хранилища Azure, содержащий файл задания Spark hello, зависимости и журналы.</span><span class="sxs-lookup"><span data-stu-id="98caf-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="98caf-3041">Если значение этого свойства не указано, используется хранилище hello, связанное с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98caf-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="98caf-3042">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="98caf-3043">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="98caf-3044">Обратите внимание hello после точки.</span><span class="sxs-lookup"><span data-stu-id="98caf-3044">Note hello following points:</span></span> 

- <span data-ttu-id="98caf-3045">Hello **тип** задано слишком**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="98caf-3046">Hello **rootPath** задано слишком**adfspark\\pyFiles** где adfspark — контейнер больших двоичных объектов Azure hello и pyFiles — нормально папки в этом контейнере.</span><span class="sxs-lookup"><span data-stu-id="98caf-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="98caf-3047">В этом примере hello хранилища больших двоичных объектов — hello, связанная с кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="98caf-3048">Вы можете отправить файл tooa hello другое хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="98caf-3049">Если сделать это, создайте toolink службы хранилища Azure связаны этой фабрики данных toohello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="98caf-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="98caf-3050">Укажите имя hello hello связаны службы как значение для hello **sparkJobLinkedService** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="98caf-3051">В разделе [свойства действия Spark](#spark-activity-properties) подробные сведения об этом и других свойствах, поддерживаемых hello Spark действия.</span><span class="sxs-lookup"><span data-stu-id="98caf-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="98caf-3052">Hello **entryFilePath** задано toohello **test.py**, который является файлом python hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="98caf-3053">Hello **getDebugInfo** задано слишком**всегда**, что означает, файлы журнала hello всегда создается (успех или сбой).</span><span class="sxs-lookup"><span data-stu-id="98caf-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="98caf-3054">Мы рекомендуем, что не задано это свойство tooAlways в рабочей среде, если нужно устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="98caf-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="98caf-3055">Hello **выводит** раздел содержит один выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="98caf-3056">Необходимо указать выходной набор данных, даже если программа spark hello не создает никаких выходных данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="98caf-3057">Hello выходного набора данных дисков hello расписания для конвейера hello (каждый час, день, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="98caf-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="98caf-3058">Дополнительные сведения о действии hello см. в разделе [действия Spark](data-factory-spark.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="98caf-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="98caf-3059">Действие выполнения пакета в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="98caf-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="98caf-3060">Можно указать следующие свойства в определении Azure ML пакетного выполнения действия JSON hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="98caf-3061">свойство типа Hello для действия "hello" должно быть: **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="98caf-3062">Необходимо создать Azure машинного обучения связанной службы сначала и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-3063">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooAzureMLBatchExecution действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="98caf-3064">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-3064">Property</span></span> | <span data-ttu-id="98caf-3065">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-3065">Description</span></span> | <span data-ttu-id="98caf-3066">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="98caf-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="98caf-3067">webServiceInput</span></span> | <span data-ttu-id="98caf-3068">набор данных toobe Hello передана в качестве входных данных для веб-службы машинного Обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="98caf-3069">Этот набор данных также должно быть включено в hello входные данные для действия "hello".</span><span class="sxs-lookup"><span data-stu-id="98caf-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="98caf-3070">Используйте webServiceInput или webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="98caf-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="98caf-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="98caf-3071">webServiceInputs</span></span> | <span data-ttu-id="98caf-3072">Укажите toobe наборы данных, переданные как входные данные для hello веб-службы машинного Обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="98caf-3073">Если веб-служба hello принимает несколько входов, свойство hello webServiceInputs вместо того чтобы использовать свойство webServiceInput hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="98caf-3074">Наборы данных, на которые ссылается hello **webServiceInputs** также должны быть включены в действие hello **входов**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="98caf-3075">Используйте webServiceInput или webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="98caf-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="98caf-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="98caf-3076">webServiceOutputs</span></span> | <span data-ttu-id="98caf-3077">Hello наборы данных, которые были назначены в качестве выходных данных для веб-службы машинного Обучения Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="98caf-3078">Hello веб-служба возвращает выходные данные в этом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="98caf-3079">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3079">Yes</span></span> | 
<span data-ttu-id="98caf-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-3080">globalParameters</span></span> | <span data-ttu-id="98caf-3081">Укажите значения для hello параметры веб-службы в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="98caf-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="98caf-3082">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="98caf-3083">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3083">JSON example</span></span>
<span data-ttu-id="98caf-3084">В этом примере hello действие имеет набор данных hello **MLSqlInput** в качестве входного и **MLSqlOutput** в качестве выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="98caf-3085">Hello **MLSqlInput** передается в качестве входного toohello веб-службы с помощью hello **webServiceInput** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="98caf-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="98caf-3086">Hello **MLSqlOutput** передается в качестве выходных данных toohello веб-службы с помощью hello **webServiceOutputs** свойства JSON.</span><span class="sxs-lookup"><span data-stu-id="98caf-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="98caf-3087">В примере JSON hello hello развернута служба использует средство чтения и записи модуля tooread и записи данных из компьютер обучения Azure веб-tooan базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="98caf-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="98caf-3088">Этот веб-служба предоставляет hello следующие четыре параметра: имя сервера, имя базы данных, имя учетной записи пользователя сервера и пароль учетной записи пользователя сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="98caf-3089">Только входные и выходные данные действия AzureMLBatchExecution hello могут передаваться как параметры toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="98caf-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="98caf-3090">Например в hello выше фрагменте кода JSON MLSqlInput является входной toohello AzureMLBatchExecution действия, которое передается в качестве входного toohello веб-службы через параметр webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="98caf-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="98caf-3091">Действие обновления ресурса в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="98caf-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="98caf-3092">Можно указать следующие свойства в определении Azure ML обновление ресурсов действии JSON hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="98caf-3093">свойство типа Hello для действия "hello" должно быть: **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="98caf-3094">Необходимо создать Azure машинного обучения связанной службы сначала и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-3095">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooAzureMLUpdateResource действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="98caf-3096">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-3096">Property</span></span> | <span data-ttu-id="98caf-3097">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-3097">Description</span></span> | <span data-ttu-id="98caf-3098">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="98caf-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="98caf-3099">trainedModelName</span></span> | <span data-ttu-id="98caf-3100">Имя hello повторное Обучение модели.</span><span class="sxs-lookup"><span data-stu-id="98caf-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="98caf-3101">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3101">Yes</span></span> |  
<span data-ttu-id="98caf-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="98caf-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="98caf-3103">Файл набора данных указывающего toohello iLearner возвращенных hello переподготовки операции.</span><span class="sxs-lookup"><span data-stu-id="98caf-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="98caf-3104">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="98caf-3105">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3105">JSON example</span></span>
<span data-ttu-id="98caf-3106">Hello конвейера содержит два действия: **AzureMLBatchExecution** и **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="98caf-3107">Hello операции при выполнении пакета машинного Обучения Azure принимает hello обучающие данные в качестве входных данных и создает файл iLearner, как выходные данные.</span><span class="sxs-lookup"><span data-stu-id="98caf-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="98caf-3108">Действие Hello вызывает hello обучения веб-службы (эксперимента обучения в виде веб-службы) с входными данными hello обучающих данных и получает от веб-службы hello файл ilearner hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="98caf-3109">Hello placeholderBlob является просто пустой результирующий набор данных, которые требуются для конвейера hello toorun служба фабрики данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="98caf-3110">Действие U-SQL в аналитике озера данных</span><span class="sxs-lookup"><span data-stu-id="98caf-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="98caf-3111">Можно указать следующие свойства в определении JSON действия U-SQL hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="98caf-3112">свойство типа Hello для действия "hello" должно быть: **DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="98caf-3113">Необходимо создать службу связанной аналитики Озера данных Azure и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-3114">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа действия tooDataLakeAnalyticsU-SQL:</span><span class="sxs-lookup"><span data-stu-id="98caf-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="98caf-3115">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-3115">Property</span></span> | <span data-ttu-id="98caf-3116">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-3116">Description</span></span> | <span data-ttu-id="98caf-3117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="98caf-3118">scriptPath</span></span> |<span data-ttu-id="98caf-3119">Toofolder путь, содержащий скрипт hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="98caf-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="98caf-3120">Имя файла hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="98caf-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="98caf-3121">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="98caf-3121">No (if you use script)</span></span> |
| <span data-ttu-id="98caf-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="98caf-3122">scriptLinkedService</span></span> |<span data-ttu-id="98caf-3123">Связанной службы, которая связывает hello хранилища, содержащий фабрики данных toohello сценария hello</span><span class="sxs-lookup"><span data-stu-id="98caf-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="98caf-3124">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="98caf-3124">No (if you use script)</span></span> |
| <span data-ttu-id="98caf-3125">script</span><span class="sxs-lookup"><span data-stu-id="98caf-3125">script</span></span> |<span data-ttu-id="98caf-3126">Указание сценария непосредственно в строке вместо использования scriptPath и scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="98caf-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="98caf-3127">Например: "script" : "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="98caf-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="98caf-3128">Нет (при использовании scriptPath и scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="98caf-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="98caf-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="98caf-3129">degreeOfParallelism</span></span> |<span data-ttu-id="98caf-3130">Максимальное количество узлов Hello одновременно использовать toorun hello задания.</span><span class="sxs-lookup"><span data-stu-id="98caf-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="98caf-3131">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3131">No</span></span> |
| <span data-ttu-id="98caf-3132">priority</span><span class="sxs-lookup"><span data-stu-id="98caf-3132">priority</span></span> |<span data-ttu-id="98caf-3133">Определяет, какие задания из всех, поставленных в очередь должна быть выбранного toorun сначала.</span><span class="sxs-lookup"><span data-stu-id="98caf-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="98caf-3134">Hello hello снижать hello более высокий приоритет hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="98caf-3135">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3135">No</span></span> |
| <span data-ttu-id="98caf-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="98caf-3136">parameters</span></span> |<span data-ttu-id="98caf-3137">Параметры для скрипта hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="98caf-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="98caf-3138">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="98caf-3139">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="98caf-3140">Дополнительные сведения см. в статье о [действии U-SQL Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="98caf-3141">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="98caf-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="98caf-3142">Можно указать следующие свойства в определении хранимой процедуры действии JSON hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="98caf-3143">свойство типа Hello для действия "hello" должно быть: **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="98caf-3144">Необходимо создать следующие связанные службы hello и указывать имя hello hello связаны службы в качестве значения для hello **linkedServiceName** свойства:</span><span class="sxs-lookup"><span data-stu-id="98caf-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="98caf-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="98caf-3145">SQL Server</span></span> 
- <span data-ttu-id="98caf-3146">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-3146">Azure SQL Database</span></span>
- <span data-ttu-id="98caf-3147">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="98caf-3148">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooSqlServerStoredProcedure действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="98caf-3149">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-3149">Property</span></span> | <span data-ttu-id="98caf-3150">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-3150">Description</span></span> | <span data-ttu-id="98caf-3151">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="98caf-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="98caf-3152">storedProcedureName</span></span> |<span data-ttu-id="98caf-3153">Укажите имя hello hello хранимой процедуры в базе данных Azure SQL hello или хранилище данных SQL Azure, представленного hello связаны службы, которая hello использования выходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="98caf-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="98caf-3154">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3154">Yes</span></span> |
| <span data-ttu-id="98caf-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="98caf-3155">storedProcedureParameters</span></span> |<span data-ttu-id="98caf-3156">Указываемые значения для параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="98caf-3157">Если вам требуется toopass значение null для параметра, используйте синтаксис hello: «param1»: null (все строчные).</span><span class="sxs-lookup"><span data-stu-id="98caf-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="98caf-3158">См. следующий пример toolearn об использовании этого свойства hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="98caf-3159">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3159">No</span></span> |

<span data-ttu-id="98caf-3160">При указании входного набора данных, он должен быть доступен (в состояние «Готово») для hello хранимой процедуры toorun действия.</span><span class="sxs-lookup"><span data-stu-id="98caf-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="98caf-3161">Hello входного набора данных не может использоваться в hello хранимой процедуре как параметр.</span><span class="sxs-lookup"><span data-stu-id="98caf-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="98caf-3162">Это только используемые toocheck hello зависимостей, до начала hello действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="98caf-3163">Для действия хранимой процедуры необходимо указать выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="98caf-3164">Выходной набор данных указывает hello **расписание** для hello действие хранимой процедуры (каждый час, еженедельно, ежемесячно, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="98caf-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="98caf-3165">Hello выходной набор данных необходимо использовать **связанная служба** , обозначающий tooan базы данных SQL Azure или хранилище данных SQL Azure или базе SQL Server, в котором нужно hello toorun хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="98caf-3166">Hello выходной набор данных может служить результат hello toopass способом hello хранимые процедуры для последующей обработки другим действием ([цепочки действий](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="98caf-3167">Однако фабрики данных вывода автоматически hello объекта dataset toothis хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="98caf-3168">Это hello хранимая процедура записи таблицы tooa SQL, который hello указывает выходного набора данных.</span><span class="sxs-lookup"><span data-stu-id="98caf-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="98caf-3169">В некоторых случаях может быть выходной набор данных hello **пустой набор данных**, который используется только для hello расписание hello toospecify действие хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="98caf-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="98caf-3170">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="98caf-3171">Дополнительные сведения см. в статье о [действии хранимой процедуры](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="98caf-3172">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="98caf-3172">.NET custom activity</span></span>
<span data-ttu-id="98caf-3173">Можно указать следующие свойства в настраиваемом действии .NET определения JSON hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="98caf-3174">свойство типа Hello для действия "hello" должно быть: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="98caf-3175">Необходимо создать связанная служба Azure HDInsight или связанной Azure пакетной службе и задайте имя hello hello связаны службы как значение для hello **linkedServiceName** свойство.</span><span class="sxs-lookup"><span data-stu-id="98caf-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="98caf-3176">Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooDotNetActivity действия:</span><span class="sxs-lookup"><span data-stu-id="98caf-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="98caf-3177">Свойство</span><span class="sxs-lookup"><span data-stu-id="98caf-3177">Property</span></span> | <span data-ttu-id="98caf-3178">Описание</span><span class="sxs-lookup"><span data-stu-id="98caf-3178">Description</span></span> | <span data-ttu-id="98caf-3179">Обязательно</span><span class="sxs-lookup"><span data-stu-id="98caf-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="98caf-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="98caf-3180">AssemblyName</span></span> | <span data-ttu-id="98caf-3181">Имя сборки hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3181">Name of hello assembly.</span></span> <span data-ttu-id="98caf-3182">В примере hello: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="98caf-3183">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3183">Yes</span></span> |
| <span data-ttu-id="98caf-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="98caf-3184">EntryPoint</span></span> |<span data-ttu-id="98caf-3185">Имя класса "hello", реализующий интерфейс IDotNetActivity hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="98caf-3186">В примере hello: **MyDotNetActivityNS.MyDotNetActivity** где MyDotNetActivityNS является пространством имен hello и MyDotNetActivity является классом hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="98caf-3187">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3187">Yes</span></span> | 
| <span data-ttu-id="98caf-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="98caf-3188">PackageLinkedService</span></span> | <span data-ttu-id="98caf-3189">Имя связанной службой хранилища Azure, указывающий toohello хранилища больших двоичных объектов, содержащий ZIP-файл hello пользовательское действие hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="98caf-3190">В примере hello: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="98caf-3191">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3191">Yes</span></span> |
| <span data-ttu-id="98caf-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="98caf-3192">PackageFile</span></span> | <span data-ttu-id="98caf-3193">Имя hello ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="98caf-3193">Name of hello zip file.</span></span> <span data-ttu-id="98caf-3194">В примере hello: **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="98caf-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="98caf-3195">Да</span><span class="sxs-lookup"><span data-stu-id="98caf-3195">Yes</span></span> |
| <span data-ttu-id="98caf-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="98caf-3196">extendedProperties</span></span> | <span data-ttu-id="98caf-3197">Расширенные свойства, которые вы можете определять и передавать на коде .NET toohello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="98caf-3198">В этом примере hello **SliceStart** переменной задано значение tooa на основании hello SliceStart системной переменной.</span><span class="sxs-lookup"><span data-stu-id="98caf-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="98caf-3199">Нет</span><span class="sxs-lookup"><span data-stu-id="98caf-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="98caf-3200">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="98caf-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="98caf-3201">Подробные сведения см. в статье об [использовании настраиваемых действий в фабрике данных](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="98caf-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="98caf-3202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98caf-3202">Next Steps</span></span>
<span data-ttu-id="98caf-3203">См. следующие учебники hello.</span><span class="sxs-lookup"><span data-stu-id="98caf-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="98caf-3204">Руководство. Создание конвейера с действием копирования с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="98caf-3205">Руководство. Создание первой фабрики данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="98caf-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)