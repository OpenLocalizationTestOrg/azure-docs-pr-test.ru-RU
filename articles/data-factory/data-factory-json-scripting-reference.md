---
title: "Справочник по написанию скриптов JSON фабрики данных Azure | Документация Майкрософт"
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
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="40635-103">Справочник по написанию скриптов JSON фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="40635-104">Эта статья содержит схемы JSON и примеры для определения сущностей фабрики данных Azure (конвейер, действие, набор данных и связанная служба).</span><span class="sxs-lookup"><span data-stu-id="40635-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="40635-105">Конвейер</span><span class="sxs-lookup"><span data-stu-id="40635-105">Pipeline</span></span> 
<span data-ttu-id="40635-106">Высокоуровневая структура определения конвейера выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40635-106">The high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="40635-107">В приведенной ниже таблице описаны свойства, используемые в определениях JSON конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="40635-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-108">Property</span></span> | <span data-ttu-id="40635-109">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-109">Description</span></span> | <span data-ttu-id="40635-110">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="40635-111">name</span><span class="sxs-lookup"><span data-stu-id="40635-111">name</span></span> | <span data-ttu-id="40635-112">Имя конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-112">Name of the pipeline.</span></span> <span data-ttu-id="40635-113">Укажите имя, представляющее операцию, для выполнения которой настроено действие или конвейер.</span><span class="sxs-lookup"><span data-stu-id="40635-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="40635-114">Максимальное количество знаков: 260.</span><span class="sxs-lookup"><span data-stu-id="40635-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="40635-115">Должно начинаться с буквы, цифры или символа подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="40635-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="40635-116">Следующие знаки не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="40635-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="40635-117">Да</span><span class="sxs-lookup"><span data-stu-id="40635-117">Yes</span></span> |
| <span data-ttu-id="40635-118">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-118">description</span></span> |<span data-ttu-id="40635-119">Текст, описывающий, для чего используется действие или конвейер</span><span class="sxs-lookup"><span data-stu-id="40635-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="40635-120">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-120">No</span></span> |
| <span data-ttu-id="40635-121">Действия</span><span class="sxs-lookup"><span data-stu-id="40635-121">activities</span></span> | <span data-ttu-id="40635-122">Содержит список действий.</span><span class="sxs-lookup"><span data-stu-id="40635-122">Contains a list of activities.</span></span> | <span data-ttu-id="40635-123">Да</span><span class="sxs-lookup"><span data-stu-id="40635-123">Yes</span></span> |
| <span data-ttu-id="40635-124">start</span><span class="sxs-lookup"><span data-stu-id="40635-124">start</span></span> |<span data-ttu-id="40635-125">Дата и время начала работы конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="40635-126">Задается в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="40635-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="40635-127">Например: 2014-10-14T16:32:41.</span><span class="sxs-lookup"><span data-stu-id="40635-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="40635-128">Можно указать местное время, например восточное поясное время (EST).</span><span class="sxs-lookup"><span data-stu-id="40635-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="40635-129">Пример: `2016-02-27T06:00:00**-05:00`. Это 6:00 по восточному стандартному времени.</span><span class="sxs-lookup"><span data-stu-id="40635-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="40635-130">Свойства start и end определяют активный период работы конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="40635-131">Срезы выходных данных создаются только в этот активный период.</span><span class="sxs-lookup"><span data-stu-id="40635-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="40635-132">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-132">No</span></span><br/><br/><span data-ttu-id="40635-133">Если вы указываете значение свойства end, вы также должны указать значение свойства start.</span><span class="sxs-lookup"><span data-stu-id="40635-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="40635-134">Для создания конвейера значения времени начала и времени окончания могут быть пустыми.</span><span class="sxs-lookup"><span data-stu-id="40635-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="40635-135">Если требуется задать активный период работы конвейера, следует указать оба значения.</span><span class="sxs-lookup"><span data-stu-id="40635-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="40635-136">Если вы не указали время начала и окончания при создании конвейера, их можно установить позже с помощью командлета Set-AzureRmDataFactoryPipelineActivePeriod.</span><span class="sxs-lookup"><span data-stu-id="40635-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="40635-137">end</span><span class="sxs-lookup"><span data-stu-id="40635-137">end</span></span> |<span data-ttu-id="40635-138">Дата и время завершения работы конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-138">End date-time for the pipeline.</span></span> <span data-ttu-id="40635-139">Не является обязательным и задается в формате ISO.</span><span class="sxs-lookup"><span data-stu-id="40635-139">If specified must be in ISO format.</span></span> <span data-ttu-id="40635-140">Например: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="40635-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="40635-141">Можно указать местное время, например восточное поясное время (EST).</span><span class="sxs-lookup"><span data-stu-id="40635-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="40635-142">Пример: `2016-02-27T06:00:00**-05:00`. Это 6:00 по восточному стандартному времени.</span><span class="sxs-lookup"><span data-stu-id="40635-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="40635-143">Чтобы работа конвейера не была ограничена во времени, укажите для свойства end значение 9999-09-09.</span><span class="sxs-lookup"><span data-stu-id="40635-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="40635-144">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-144">No</span></span> <br/><br/><span data-ttu-id="40635-145">Если вы указываете значение свойства end, вы также должны указать значение свойства start.</span><span class="sxs-lookup"><span data-stu-id="40635-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="40635-146">Ознакомьтесь с примечаниями к свойству **start**.</span><span class="sxs-lookup"><span data-stu-id="40635-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="40635-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="40635-147">isPaused</span></span> |<span data-ttu-id="40635-148">Если задано значение true, конвейер не запускается.</span><span class="sxs-lookup"><span data-stu-id="40635-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="40635-149">Значение по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="40635-149">Default value = false.</span></span> <span data-ttu-id="40635-150">Это свойство можно использовать для включения или отключения.</span><span class="sxs-lookup"><span data-stu-id="40635-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="40635-151">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-151">No</span></span> |
| <span data-ttu-id="40635-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="40635-152">pipelineMode</span></span> |<span data-ttu-id="40635-153">Определяет метод планирования работы конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="40635-154">Допустимые значения: scheduled (по умолчанию), onetime.</span><span class="sxs-lookup"><span data-stu-id="40635-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="40635-155">Значение scheduled означает, что конвейер будет запускаться с указанной периодичностью в соответствии с его активным периодом (временем начала и окончания).</span><span class="sxs-lookup"><span data-stu-id="40635-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="40635-156">Значение onetime означает, что конвейер будет запускаться только один раз.</span><span class="sxs-lookup"><span data-stu-id="40635-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="40635-157">В настоящее время изменить или обновить однократные конвейеры после их создания нельзя.</span><span class="sxs-lookup"><span data-stu-id="40635-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="40635-158">Подробные сведения об однократном запуске см. в разделе [Однократный конвейер](data-factory-create-pipelines.md#onetime-pipeline).</span><span class="sxs-lookup"><span data-stu-id="40635-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="40635-159">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-159">No</span></span> |
| <span data-ttu-id="40635-160">expirationTime;</span><span class="sxs-lookup"><span data-stu-id="40635-160">expirationTime</span></span> |<span data-ttu-id="40635-161">Период времени после создания, в течение которого конвейер является допустимым и должен оставаться подготовленным.</span><span class="sxs-lookup"><span data-stu-id="40635-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="40635-162">Если на момент завершения этого периода у конвейера не будет активных, невыполненных или ожидающих выполнения запусков, конвейер будет автоматически удален.</span><span class="sxs-lookup"><span data-stu-id="40635-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="40635-163">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="40635-164">Действие</span><span class="sxs-lookup"><span data-stu-id="40635-164">Activity</span></span> 
<span data-ttu-id="40635-165">Высокоуровневая структура действия в рамках определения конвейера (элемент действий) выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40635-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="40635-166">В приведенной ниже таблице описаны свойства, используемые в определениях JSON действия.</span><span class="sxs-lookup"><span data-stu-id="40635-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="40635-167">Тег</span><span class="sxs-lookup"><span data-stu-id="40635-167">Tag</span></span> | <span data-ttu-id="40635-168">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-168">Description</span></span> | <span data-ttu-id="40635-169">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-170">name</span><span class="sxs-lookup"><span data-stu-id="40635-170">name</span></span> |<span data-ttu-id="40635-171">Имя действия.</span><span class="sxs-lookup"><span data-stu-id="40635-171">Name of the activity.</span></span> <span data-ttu-id="40635-172">Укажите имя, представляющее операцию, для выполнения которой настроено действие.</span><span class="sxs-lookup"><span data-stu-id="40635-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="40635-173">Максимальное количество знаков: 260.</span><span class="sxs-lookup"><span data-stu-id="40635-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="40635-174">Должно начинаться с буквы, цифры или символа подчеркивания (_).</span><span class="sxs-lookup"><span data-stu-id="40635-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="40635-175">Следующие знаки не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</span><span class="sxs-lookup"><span data-stu-id="40635-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="40635-176">Да</span><span class="sxs-lookup"><span data-stu-id="40635-176">Yes</span></span> |
| <span data-ttu-id="40635-177">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-177">description</span></span> |<span data-ttu-id="40635-178">Текст, описывающий для чего используется действие</span><span class="sxs-lookup"><span data-stu-id="40635-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="40635-179">Да</span><span class="sxs-lookup"><span data-stu-id="40635-179">Yes</span></span> |
| <span data-ttu-id="40635-180">type</span><span class="sxs-lookup"><span data-stu-id="40635-180">type</span></span> |<span data-ttu-id="40635-181">Задает тип действия.</span><span class="sxs-lookup"><span data-stu-id="40635-181">Specifies the type of the activity.</span></span> <span data-ttu-id="40635-182">Разные типы действий описаны в разделах [ХРАНИЛИЩА ДАННЫХ](#data-stores) и [Действия преобразования данных](#data-transformation-activities).</span><span class="sxs-lookup"><span data-stu-id="40635-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="40635-183">Да</span><span class="sxs-lookup"><span data-stu-id="40635-183">Yes</span></span> |
| <span data-ttu-id="40635-184">inputs</span><span class="sxs-lookup"><span data-stu-id="40635-184">inputs</span></span> |<span data-ttu-id="40635-185">Входные таблицы, используемые действием:</span><span class="sxs-lookup"><span data-stu-id="40635-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="40635-186">Да</span><span class="sxs-lookup"><span data-stu-id="40635-186">Yes</span></span> |
| <span data-ttu-id="40635-187">outputs</span><span class="sxs-lookup"><span data-stu-id="40635-187">outputs</span></span> |<span data-ttu-id="40635-188">Выходные таблицы, используемые действием.</span><span class="sxs-lookup"><span data-stu-id="40635-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="40635-189">Да</span><span class="sxs-lookup"><span data-stu-id="40635-189">Yes</span></span> |
| <span data-ttu-id="40635-190">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="40635-190">linkedServiceName</span></span> |<span data-ttu-id="40635-191">Имя связанной службы, используемой действием.</span><span class="sxs-lookup"><span data-stu-id="40635-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="40635-192">Для действия может потребоваться указать службу, связанную с обязательной вычислительной средой.</span><span class="sxs-lookup"><span data-stu-id="40635-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="40635-193">Да, для действий HDInsight, Машинного обучения Azure и действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="40635-194">Нет — для всех остальных</span><span class="sxs-lookup"><span data-stu-id="40635-194">No for all others</span></span> |
| <span data-ttu-id="40635-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="40635-195">typeProperties</span></span> |<span data-ttu-id="40635-196">Свойства в разделе typeProperties зависят от типа действия.</span><span class="sxs-lookup"><span data-stu-id="40635-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="40635-197">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-197">No</span></span> |
| <span data-ttu-id="40635-198">policy</span><span class="sxs-lookup"><span data-stu-id="40635-198">policy</span></span> |<span data-ttu-id="40635-199">Политики, которые влияют на поведение во время выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="40635-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="40635-200">Если для этого свойства не задано значение, используются стандартные политики.</span><span class="sxs-lookup"><span data-stu-id="40635-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="40635-201">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-201">No</span></span> |
| <span data-ttu-id="40635-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="40635-202">scheduler</span></span> |<span data-ttu-id="40635-203">Свойство scheduler позволяет задать расписание выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="40635-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="40635-204">Для него предусмотрен такой же набор подсвойств, что и для [свойства availability в наборе данных](data-factory-create-datasets.md#dataset-availability).</span><span class="sxs-lookup"><span data-stu-id="40635-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="40635-205">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="40635-206">Политики</span><span class="sxs-lookup"><span data-stu-id="40635-206">Policies</span></span>
<span data-ttu-id="40635-207">Политики влияют на поведение во время выполнения действия, особенно при обработке среза таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="40635-208">В следующей таблице приведено несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="40635-208">The following table provides the details.</span></span>

| <span data-ttu-id="40635-209">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-209">Property</span></span> | <span data-ttu-id="40635-210">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-210">Permitted values</span></span> | <span data-ttu-id="40635-211">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="40635-211">Default Value</span></span> | <span data-ttu-id="40635-212">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-213">concurrency</span><span class="sxs-lookup"><span data-stu-id="40635-213">concurrency</span></span> |<span data-ttu-id="40635-214">Целое число </span><span class="sxs-lookup"><span data-stu-id="40635-214">Integer</span></span> <br/><br/><span data-ttu-id="40635-215">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="40635-215">Max value: 10</span></span> |<span data-ttu-id="40635-216">1</span><span class="sxs-lookup"><span data-stu-id="40635-216">1</span></span> |<span data-ttu-id="40635-217">Число одновременных выполнений действия.</span><span class="sxs-lookup"><span data-stu-id="40635-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="40635-218">Определяет количество параллельных выполнений одного действия для обработки разных срезов.</span><span class="sxs-lookup"><span data-stu-id="40635-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="40635-219">Например, высокое значение этого свойства ускорит обработку большого набора доступных данных.</span><span class="sxs-lookup"><span data-stu-id="40635-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="40635-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="40635-220">executionPriorityOrder</span></span> |<span data-ttu-id="40635-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="40635-221">NewestFirst</span></span><br/><br/><span data-ttu-id="40635-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="40635-222">OldestFirst</span></span> |<span data-ttu-id="40635-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="40635-223">OldestFirst</span></span> |<span data-ttu-id="40635-224">Определяет порядок обработки срезов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="40635-225">Предположим, есть два ожидающих обработки среза (от 16:00 и от 17:00).</span><span class="sxs-lookup"><span data-stu-id="40635-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="40635-226">Если для свойства executionPriorityOrder задано значение NewestFirst, срез от 17:00 будет обработан первым.</span><span class="sxs-lookup"><span data-stu-id="40635-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="40635-227">Точно так же, если для executionPriorityORder задано значение OldestFIrst, первым будет обработан срез от 16:00.</span><span class="sxs-lookup"><span data-stu-id="40635-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="40635-228">retry</span><span class="sxs-lookup"><span data-stu-id="40635-228">retry</span></span> |<span data-ttu-id="40635-229">Целое число </span><span class="sxs-lookup"><span data-stu-id="40635-229">Integer</span></span><br/><br/><span data-ttu-id="40635-230">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="40635-230">Max value can be 10</span></span> |<span data-ttu-id="40635-231">0</span><span class="sxs-lookup"><span data-stu-id="40635-231">0</span></span> |<span data-ttu-id="40635-232">Число повторных попыток обработки данных до того, как срез перейдет в состояние Failure (сбой).</span><span class="sxs-lookup"><span data-stu-id="40635-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="40635-233">Выполнение действия со срезом данных повторяется указанное количество раз.</span><span class="sxs-lookup"><span data-stu-id="40635-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="40635-234">Повторная попытка выполняется сразу после неудачной.</span><span class="sxs-lookup"><span data-stu-id="40635-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="40635-235">timeout</span><span class="sxs-lookup"><span data-stu-id="40635-235">timeout</span></span> |<span data-ttu-id="40635-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="40635-236">TimeSpan</span></span> |<span data-ttu-id="40635-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="40635-237">00:00:00</span></span> |<span data-ttu-id="40635-238">Время ожидания для действия.</span><span class="sxs-lookup"><span data-stu-id="40635-238">Timeout for the activity.</span></span> <span data-ttu-id="40635-239">Пример: 00:10:00 (время ожидания — 10 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="40635-240">Если значение не указано или равно 0, то время ожидания не ограничено.</span><span class="sxs-lookup"><span data-stu-id="40635-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="40635-241">Если время обработки среза превышает время ожидания, система отменяет текущую обработку и начинает новую.</span><span class="sxs-lookup"><span data-stu-id="40635-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="40635-242">Количество повторов зависит от значения свойства retry.</span><span class="sxs-lookup"><span data-stu-id="40635-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="40635-243">Когда время ожидания истекает, состояние среза меняется на TimedOut.</span><span class="sxs-lookup"><span data-stu-id="40635-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="40635-244">delay</span><span class="sxs-lookup"><span data-stu-id="40635-244">delay</span></span> |<span data-ttu-id="40635-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="40635-245">TimeSpan</span></span> |<span data-ttu-id="40635-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="40635-246">00:00:00</span></span> |<span data-ttu-id="40635-247">Задайте задержку перед обработкой данных после начала выполнения среза.</span><span class="sxs-lookup"><span data-stu-id="40635-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="40635-248">Действие для среза данных запускается в ожидаемое время выполнения с указанной задержкой.</span><span class="sxs-lookup"><span data-stu-id="40635-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="40635-249">Пример: 00:10:00 (означает задержку в 10 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="40635-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="40635-250">longRetry</span></span> |<span data-ttu-id="40635-251">Целое число </span><span class="sxs-lookup"><span data-stu-id="40635-251">Integer</span></span><br/><br/><span data-ttu-id="40635-252">Максимальное значение — 10</span><span class="sxs-lookup"><span data-stu-id="40635-252">Max value: 10</span></span> |<span data-ttu-id="40635-253">1</span><span class="sxs-lookup"><span data-stu-id="40635-253">1</span></span> |<span data-ttu-id="40635-254">Количество длительных повторных попыток перед завершением сбоем выполнения среза.</span><span class="sxs-lookup"><span data-stu-id="40635-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="40635-255">Интервал между этими попытками задается свойством longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="40635-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="40635-256">Используйте свойство longRetry, если повторные попытки необходимо выполнять с паузами.</span><span class="sxs-lookup"><span data-stu-id="40635-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="40635-257">Если указаны свойства Retry и longRetry, то каждая попытка longRetry включает в себя попытки Retry, и максимальное число попыток равно Retry * longRetry.</span><span class="sxs-lookup"><span data-stu-id="40635-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="40635-258">Например, в политике действия указаны следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="40635-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="40635-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="40635-259">Retry: 3</span></span><br/><span data-ttu-id="40635-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="40635-260">longRetry: 2</span></span><br/><span data-ttu-id="40635-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="40635-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="40635-262">Предположим, что существует только один выполняемый срез (в состоянии Waiting), и каждый раз при выполнении действия происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="40635-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="40635-263">Первые три попытки будут выполнены подряд.</span><span class="sxs-lookup"><span data-stu-id="40635-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="40635-264">После каждой повторной попытки срез будет находиться в состоянии Retry.</span><span class="sxs-lookup"><span data-stu-id="40635-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="40635-265">После выполнения первых трех попыток состоянием среза станет LongRetry.</span><span class="sxs-lookup"><span data-stu-id="40635-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="40635-266">Через час (значение свойства longRetryInterval) будут выполнены еще три попытки подряд.</span><span class="sxs-lookup"><span data-stu-id="40635-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="40635-267">После этого состояние среза изменится на Failed и дальнейшие попытки предприниматься не будут.</span><span class="sxs-lookup"><span data-stu-id="40635-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="40635-268">Поэтому всего было предпринято 6 попыток.</span><span class="sxs-lookup"><span data-stu-id="40635-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="40635-269">Если какое-либо выполнение завершится успешно, то состоянием среза станет Ready и дальнейшие попытки выполняться не будут.</span><span class="sxs-lookup"><span data-stu-id="40635-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="40635-270">Свойство longRetry можно использовать в ситуациях, когда зависимые данные поступают в неопределенное время или вся среда, в которой происходит обработка данных, непредсказуема.</span><span class="sxs-lookup"><span data-stu-id="40635-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="40635-271">В таких случаях последовательные повторные попытки могут оказаться бесполезными, а выполненные через некоторое время, напротив, могут привести к желаемому результату.</span><span class="sxs-lookup"><span data-stu-id="40635-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="40635-272">Предупреждение. Не задавайте высокие значения для свойств longRetry и longRetryInterval.</span><span class="sxs-lookup"><span data-stu-id="40635-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="40635-273">Как правило, более высокие значения приводят к появлению других системных проблем.</span><span class="sxs-lookup"><span data-stu-id="40635-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="40635-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="40635-274">longRetryInterval</span></span> |<span data-ttu-id="40635-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="40635-275">TimeSpan</span></span> |<span data-ttu-id="40635-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="40635-276">00:00:00</span></span> |<span data-ttu-id="40635-277">Период времени между длительными повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="40635-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="40635-278">Раздел typeProperties</span><span class="sxs-lookup"><span data-stu-id="40635-278">typeProperties section</span></span>
<span data-ttu-id="40635-279">Разделы typeProperties для каждого действия отличаются.</span><span class="sxs-lookup"><span data-stu-id="40635-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="40635-280">Действия преобразования имеют только свойства типа.</span><span class="sxs-lookup"><span data-stu-id="40635-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="40635-281">В разделе [ДЕЙСТВИЯ ПРЕОБРАЗОВАНИЯ ДАННЫХ](#data-transformation-activities) этой статьи представлены примеры JSON, определяющие действия преобразования в конвейере.</span><span class="sxs-lookup"><span data-stu-id="40635-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="40635-282">**Действие копирования** имеет два подраздела в разделе typeProperties: **source** и **sink**.</span><span class="sxs-lookup"><span data-stu-id="40635-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="40635-283">В разделе [ХРАНИЛИЩА ДАННЫХ](#data-stores) этой статьи представлены примеры JSON, в которых показано, как использовать хранилище данных как источник или приемник.</span><span class="sxs-lookup"><span data-stu-id="40635-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="40635-284">Пример конвейера копирования</span><span class="sxs-lookup"><span data-stu-id="40635-284">Sample copy pipeline</span></span>
<span data-ttu-id="40635-285">В следующем примере конвейера содержится одно действие типа **Copy** in the **действий** .</span><span class="sxs-lookup"><span data-stu-id="40635-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="40635-286">В этом примере [действие копирования](data-factory-data-movement-activities.md) копирует данные из хранилища BLOB-объектов Azure в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
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

<span data-ttu-id="40635-287">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="40635-287">Note the following points:</span></span>

* <span data-ttu-id="40635-288">В разделе действий доступно только одно действие, параметр **type** которого имеет значение **Copy**.</span><span class="sxs-lookup"><span data-stu-id="40635-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="40635-289">Для этого действия параметру input присвоено значение **InputDataset**, а параметру output — значение **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="40635-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="40635-290">В разделе **typeProperties** в качестве типа источника указано **BlobSource**, а в качестве типа приемника — **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="40635-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="40635-291">В разделе [ХРАНИЛИЩА ДАННЫХ](#data-stores) этой статьи представлены примеры JSON, в которых показано, как использовать хранилище данных как источник или приемник.</span><span class="sxs-lookup"><span data-stu-id="40635-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="40635-292">Полное пошаговое руководство по созданию этого конвейера см. в разделе [Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="40635-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="40635-293">Пример конвейера преобразования</span><span class="sxs-lookup"><span data-stu-id="40635-293">Sample transformation pipeline</span></span>
<span data-ttu-id="40635-294">В следующем примере конвейера содержится одно действие типа **HDInsightHive** in the **действий** .</span><span class="sxs-lookup"><span data-stu-id="40635-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="40635-295">В этом примере [действие HDInsight Hive](data-factory-hive-activity.md) преобразовывает данные из хранилища BLOB-объектов Azure, запуская файл сценария Hive в кластере Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="40635-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="40635-296">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="40635-296">Note the following points:</span></span> 

* <span data-ttu-id="40635-297">В разделе activities есть только одно действие, параметр **type** которого имеет значение **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="40635-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="40635-298">Файл сценария Hive, **partitionweblogs.hql**, хранится в учетной записи хранения Azure (указывается с помощью свойства scriptLinkedService, имеющего значение **AzureStorageLinkedService**) в папке **script** в контейнере **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="40635-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="40635-299">Раздел **defines** используется, чтобы указать параметры среды выполнения, передаваемые скрипту Hive в качестве значений конфигурации Hive (например, `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="40635-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="40635-300">В разделе [ДЕЙСТВИЯ ПРЕОБРАЗОВАНИЯ ДАННЫХ](#data-transformation-activities) этой статьи представлены примеры JSON, определяющие действия преобразования в конвейере.</span><span class="sxs-lookup"><span data-stu-id="40635-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="40635-301">Полное пошаговое руководство по созданию данного конвейера см. в разделе [Учебник. Создание первого конвейера для обработки данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="40635-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="40635-302">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-302">Linked service</span></span>
<span data-ttu-id="40635-303">Высокоуровневая структура определения связанной службы выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40635-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="40635-304">В приведенной ниже таблице описаны свойства, используемые в определениях JSON действия.</span><span class="sxs-lookup"><span data-stu-id="40635-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="40635-305">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-305">Property</span></span> | <span data-ttu-id="40635-306">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-306">Description</span></span> | <span data-ttu-id="40635-307">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="40635-308">name</span><span class="sxs-lookup"><span data-stu-id="40635-308">name</span></span> | <span data-ttu-id="40635-309">Имя связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-309">Name of the linked service.</span></span> | <span data-ttu-id="40635-310">Да</span><span class="sxs-lookup"><span data-stu-id="40635-310">Yes</span></span> | 
| <span data-ttu-id="40635-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="40635-311">properties - type</span></span> | <span data-ttu-id="40635-312">Тип связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-312">Type of the linked service.</span></span> <span data-ttu-id="40635-313">Например, служба хранилища Azure, база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="40635-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="40635-314">typeProperties</span></span> | <span data-ttu-id="40635-315">Раздел typeProperties содержит элементы, различные для каждого хранилища данных или вычислительной среды.</span><span class="sxs-lookup"><span data-stu-id="40635-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="40635-316">В разделе о [хранилищах данных](#datastores) указаны все связанные службы хранилищ данных, а в разделе о [вычислительных средах](#compute-environments) — все связанные службы вычислений.</span><span class="sxs-lookup"><span data-stu-id="40635-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="40635-317">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-317">Dataset</span></span> 
<span data-ttu-id="40635-318">Набор данных в фабрике Azure имеет определение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="40635-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="40635-319">В следующей таблице описаны свойства приведенного выше объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="40635-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="40635-320">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-320">Property</span></span> | <span data-ttu-id="40635-321">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-321">Description</span></span> | <span data-ttu-id="40635-322">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-322">Required</span></span> | <span data-ttu-id="40635-323">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="40635-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-324">name</span><span class="sxs-lookup"><span data-stu-id="40635-324">name</span></span> | <span data-ttu-id="40635-325">Имя набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-325">Name of the dataset.</span></span> <span data-ttu-id="40635-326">Правила именования для фабрики данных Azure описаны [здесь](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="40635-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="40635-327">Да</span><span class="sxs-lookup"><span data-stu-id="40635-327">Yes</span></span> |<span data-ttu-id="40635-328">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-328">NA</span></span> |
| <span data-ttu-id="40635-329">type</span><span class="sxs-lookup"><span data-stu-id="40635-329">type</span></span> | <span data-ttu-id="40635-330">Тип набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-330">Type of the dataset.</span></span> <span data-ttu-id="40635-331">Укажите один из типов, которые поддерживаются фабрикой данных Azure (например: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="40635-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="40635-332">В разделе [ХРАНИЛИЩА ДАННЫХ](#data-stores) представлены все хранилища данных и типы наборов данных, поддерживаемые фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="40635-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="40635-333">structure</span><span class="sxs-lookup"><span data-stu-id="40635-333">structure</span></span> | <span data-ttu-id="40635-334">Схема набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-334">Schema of the dataset.</span></span> <span data-ttu-id="40635-335">Она содержит столбцы, их типы и т. д.</span><span class="sxs-lookup"><span data-stu-id="40635-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="40635-336">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-336">No</span></span> |<span data-ttu-id="40635-337">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-337">NA</span></span> |
| <span data-ttu-id="40635-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="40635-338">typeProperties</span></span> | <span data-ttu-id="40635-339">Свойства, соответствующие выбранному типу.</span><span class="sxs-lookup"><span data-stu-id="40635-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="40635-340">В разделе [ХРАНИЛИЩА ДАННЫХ](#data-stores) указаны поддерживаемые типы и их свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="40635-341">Да</span><span class="sxs-lookup"><span data-stu-id="40635-341">Yes</span></span> |<span data-ttu-id="40635-342">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-342">NA</span></span> |
| <span data-ttu-id="40635-343">external</span><span class="sxs-lookup"><span data-stu-id="40635-343">external</span></span> | <span data-ttu-id="40635-344">Этот логический флаг указывает, создается ли набор данных конвейером фабрики данных явным образом.</span><span class="sxs-lookup"><span data-stu-id="40635-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="40635-345">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-345">No</span></span> |<span data-ttu-id="40635-346">нет</span><span class="sxs-lookup"><span data-stu-id="40635-346">false</span></span> |
| <span data-ttu-id="40635-347">availability</span><span class="sxs-lookup"><span data-stu-id="40635-347">availability</span></span> | <span data-ttu-id="40635-348">Определяет окно обработки или модель среза для создания набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="40635-349">Дополнительные сведения о модели срезов набора данных см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="40635-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="40635-350">Да</span><span class="sxs-lookup"><span data-stu-id="40635-350">Yes</span></span> |<span data-ttu-id="40635-351">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-351">NA</span></span> |
| <span data-ttu-id="40635-352">policy</span><span class="sxs-lookup"><span data-stu-id="40635-352">policy</span></span> |<span data-ttu-id="40635-353">Определяет условия, которым должен соответствовать срез данных.</span><span class="sxs-lookup"><span data-stu-id="40635-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="40635-354">Дополнительные сведения см. в разделе [Политика наборов данных](#Policy).</span><span class="sxs-lookup"><span data-stu-id="40635-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="40635-355">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-355">No</span></span> |<span data-ttu-id="40635-356">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-356">NA</span></span> |

<span data-ttu-id="40635-357">В каждом столбце раздела **structure** содержатся следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="40635-358">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-358">Property</span></span> | <span data-ttu-id="40635-359">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-359">Description</span></span> | <span data-ttu-id="40635-360">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-361">name</span><span class="sxs-lookup"><span data-stu-id="40635-361">name</span></span> |<span data-ttu-id="40635-362">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="40635-362">Name of the column.</span></span> |<span data-ttu-id="40635-363">Да</span><span class="sxs-lookup"><span data-stu-id="40635-363">Yes</span></span> |
| <span data-ttu-id="40635-364">type</span><span class="sxs-lookup"><span data-stu-id="40635-364">type</span></span> |<span data-ttu-id="40635-365">Тип данных столбца.</span><span class="sxs-lookup"><span data-stu-id="40635-365">Data type of the column.</span></span>  |<span data-ttu-id="40635-366">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-366">No</span></span> |
| <span data-ttu-id="40635-367">culture</span><span class="sxs-lookup"><span data-stu-id="40635-367">culture</span></span> |<span data-ttu-id="40635-368">Язык и региональные параметры на основе .NET, используемые при указании типа, если это тип .NET `Datetime` или `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="40635-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="40635-369">Значение по умолчанию — `en-us`.</span><span class="sxs-lookup"><span data-stu-id="40635-369">Default is `en-us`.</span></span> |<span data-ttu-id="40635-370">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-370">No</span></span> |
| <span data-ttu-id="40635-371">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-371">format</span></span> |<span data-ttu-id="40635-372">Строка формата, используемая при указании типа, если это тип .NET `Datetime` или `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="40635-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="40635-373">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-373">No</span></span> |

<span data-ttu-id="40635-374">В приведенном ниже примере набор данных содержит три столбца: `slicetimestamp`, `projectname` и `pageviews` с типом String, String и Decimal соответственно.</span><span class="sxs-lookup"><span data-stu-id="40635-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="40635-375">В таблице ниже перечислены свойства, которые можно использовать в разделе **availability**.</span><span class="sxs-lookup"><span data-stu-id="40635-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="40635-376">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-376">Property</span></span> | <span data-ttu-id="40635-377">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-377">Description</span></span> | <span data-ttu-id="40635-378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-378">Required</span></span> | <span data-ttu-id="40635-379">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="40635-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-380">frequency</span><span class="sxs-lookup"><span data-stu-id="40635-380">frequency</span></span> |<span data-ttu-id="40635-381">Указывает единицу времени, которая определяет частоту создания среза данных.</span><span class="sxs-lookup"><span data-stu-id="40635-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="40635-382"><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month.</span><span class="sxs-lookup"><span data-stu-id="40635-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="40635-383">Да</span><span class="sxs-lookup"><span data-stu-id="40635-383">Yes</span></span> |<span data-ttu-id="40635-384">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-384">NA</span></span> |
| <span data-ttu-id="40635-385">interval</span><span class="sxs-lookup"><span data-stu-id="40635-385">interval</span></span> |<span data-ttu-id="40635-386">Задает множитель для частоты.</span><span class="sxs-lookup"><span data-stu-id="40635-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="40635-387">"Интервал х частоты" определяет частоту создания срезов.</span><span class="sxs-lookup"><span data-stu-id="40635-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="40635-388">Если нужно, чтобы срез в наборе данных создавался каждый час, задайте для параметра <b>frequency</b> значение <b>Hour</b>, а для параметра <b>interval</b> — значение <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="40635-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="40635-389"><b>Примечание.</b> Если вы выбрали значение Minute для параметра Frequency, рекомендуем, чтобы интервал длился не менее 15 минут.</span><span class="sxs-lookup"><span data-stu-id="40635-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="40635-390">Да</span><span class="sxs-lookup"><span data-stu-id="40635-390">Yes</span></span> |<span data-ttu-id="40635-391">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-391">NA</span></span> |
| <span data-ttu-id="40635-392">style</span><span class="sxs-lookup"><span data-stu-id="40635-392">style</span></span> |<span data-ttu-id="40635-393">Указывает, когда выполняется срез: в начале или в конце интервала.</span><span class="sxs-lookup"><span data-stu-id="40635-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="40635-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="40635-394">StartOfInterval</span></span></li><li><span data-ttu-id="40635-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="40635-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="40635-396">Если для Frequency задано значение Month, а для Style — EndOfInterval, срез данных будет создаваться в последний день месяца.</span><span class="sxs-lookup"><span data-stu-id="40635-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="40635-397">Если для Style задано значение StartOfInterval, срез создается в первый день месяца.</span><span class="sxs-lookup"><span data-stu-id="40635-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="40635-398">Если для frequency задано значение Day, а для style — EndOfInterval, срез данных будет создаваться в последний час дня.</span><span class="sxs-lookup"><span data-stu-id="40635-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="40635-399">Если для Frequency задано значение Hour, а для Style — EndOfInterval, срез создается в конце часа.</span><span class="sxs-lookup"><span data-stu-id="40635-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="40635-400">Например, для периода с 13:00 до 14:00 срез создается в 14:00.</span><span class="sxs-lookup"><span data-stu-id="40635-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="40635-401">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-401">No</span></span> |<span data-ttu-id="40635-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="40635-402">EndOfInterval</span></span> |
| <span data-ttu-id="40635-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="40635-403">anchorDateTime</span></span> |<span data-ttu-id="40635-404">Определяет момент времени, на основе которого планировщик вычисляет границы среза набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="40635-405"><b>Примечание</b>. Если параметр AnchorDateTime содержит элементы с большей степенью детализации, чем значение параметра frequency, эти элементы игнорируются.</span><span class="sxs-lookup"><span data-stu-id="40635-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="40635-406">Например, если для <b>интервала</b> задано значение <b>ежечасно</b> (frequency = Hour, interval = 1), а <b>AnchorDateTime</b> содержит <b>минуты и секунды</b>, то <b>минуты и секунды</b> из параметра AnchorDateTime не учитываются.</span><span class="sxs-lookup"><span data-stu-id="40635-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="40635-407">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-407">No</span></span> |<span data-ttu-id="40635-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="40635-408">01/01/0001</span></span> |
| <span data-ttu-id="40635-409">offset</span><span class="sxs-lookup"><span data-stu-id="40635-409">offset</span></span> |<span data-ttu-id="40635-410">Интервал времени, на который сдвигаются начало и конец всех срезов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="40635-411"><b>Примечание</b>. Если указаны значения для обоих параметров (anchorDateTime и offset), сдвиг вычисляется с учетом обоих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="40635-412">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-412">No</span></span> |<span data-ttu-id="40635-413">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-413">NA</span></span> |

<span data-ttu-id="40635-414">В следующем примере раздел availability определяет то, что набор выходных данных создается ежечасно (или) доступен каждый час.</span><span class="sxs-lookup"><span data-stu-id="40635-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="40635-415">Раздел **policy** в определении набора данных содержит условия, которым должен соответствовать срез данных.</span><span class="sxs-lookup"><span data-stu-id="40635-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="40635-416">Имя политики</span><span class="sxs-lookup"><span data-stu-id="40635-416">Policy Name</span></span> | <span data-ttu-id="40635-417">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-417">Description</span></span> | <span data-ttu-id="40635-418">Применяется к</span><span class="sxs-lookup"><span data-stu-id="40635-418">Applied To</span></span> | <span data-ttu-id="40635-419">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-419">Required</span></span> | <span data-ttu-id="40635-420">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="40635-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="40635-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="40635-421">minimumSizeMB</span></span> |<span data-ttu-id="40635-422">Проверяет, удовлетворяют ли данные в **большом двоичном объекте Azure** требованиям к минимальному размеру (в мегабайтах).</span><span class="sxs-lookup"><span data-stu-id="40635-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="40635-423">большом двоичном объекте Azure</span><span class="sxs-lookup"><span data-stu-id="40635-423">Azure Blob</span></span> |<span data-ttu-id="40635-424">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-424">No</span></span> |<span data-ttu-id="40635-425">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-425">NA</span></span> |
| <span data-ttu-id="40635-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="40635-426">minimumRows</span></span> |<span data-ttu-id="40635-427">Проверяет, содержат ли данные в **базе данных SQL Azure** или **таблице Azure** минимально необходимое количество строк.</span><span class="sxs-lookup"><span data-stu-id="40635-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="40635-428">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-428">Azure SQL Database</span></span></li><li><span data-ttu-id="40635-429">таблице Azure</span><span class="sxs-lookup"><span data-stu-id="40635-429">Azure Table</span></span></li></ul> |<span data-ttu-id="40635-430">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-430">No</span></span> |<span data-ttu-id="40635-431">Нет данных</span><span class="sxs-lookup"><span data-stu-id="40635-431">NA</span></span> |

<span data-ttu-id="40635-432">**Пример**</span><span class="sxs-lookup"><span data-stu-id="40635-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="40635-433">Если набор данных не создается фабрикой данных Azure, он должен быть помечен как **external**.</span><span class="sxs-lookup"><span data-stu-id="40635-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="40635-434">Обычно этот параметр относится к входным данным для первого действия в конвейере, если не используется цепочка действий или конвейеров.</span><span class="sxs-lookup"><span data-stu-id="40635-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="40635-435">name</span><span class="sxs-lookup"><span data-stu-id="40635-435">Name</span></span> | <span data-ttu-id="40635-436">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-436">Description</span></span> | <span data-ttu-id="40635-437">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-437">Required</span></span> | <span data-ttu-id="40635-438">По умолчанию</span><span class="sxs-lookup"><span data-stu-id="40635-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="40635-439">dataDelay</span></span> |<span data-ttu-id="40635-440">Время задержки проверки на наличие внешних данных для определенного среза.</span><span class="sxs-lookup"><span data-stu-id="40635-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="40635-441">Например, если данные доступны ежечасно, проверку доступности внешних данных (и того, находится ли соответствующий срез в состоянии Ready) можно отложить, используя политику dataDelay.</span><span class="sxs-lookup"><span data-stu-id="40635-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="40635-442">Применяется только к настоящему времени.</span><span class="sxs-lookup"><span data-stu-id="40635-442">Only applies to the present time.</span></span>  <span data-ttu-id="40635-443">Например, если сейчас 13:00 и для dataDelay задано значение "10 минут", то проверка начинается в 13:10.</span><span class="sxs-lookup"><span data-stu-id="40635-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="40635-444">Этот параметр не влияет на срезы в прошлом (срезы, у которых параметры Slice End Time и dataDelay имеют значение раньше текущего времени), и они обрабатываются без задержки.</span><span class="sxs-lookup"><span data-stu-id="40635-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="40635-445">Время после 23:59 необходимо указать в формате `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="40635-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="40635-446">Например, чтобы задать 24 часа, не используйте формат 24:00:00; вместо этого укажите 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="40635-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="40635-447">Значение 24:00:00 обозначает 24 дня (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="40635-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="40635-448">Чтобы задать 1 день и 4 часа, укажите 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="40635-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="40635-449">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-449">No</span></span> |<span data-ttu-id="40635-450">0</span><span class="sxs-lookup"><span data-stu-id="40635-450">0</span></span> |
| <span data-ttu-id="40635-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="40635-451">retryInterval</span></span> |<span data-ttu-id="40635-452">Время ожидания после сбоя до повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="40635-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="40635-453">В случае сбоя попытки следующая попытка выполняется после retryInterval.</span><span class="sxs-lookup"><span data-stu-id="40635-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="40635-454">Предположим, что первая попытка началась в 13:00.</span><span class="sxs-lookup"><span data-stu-id="40635-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="40635-455">Если она длится одну минуту и завершается сбоем, то повторная попытка начнется в 13:02 (13:00 + время выполнения первой проверки (1 минута) + интервал повтора (1 минута)).</span><span class="sxs-lookup"><span data-stu-id="40635-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="40635-456">Срезы в прошлом обрабатываются без задержки.</span><span class="sxs-lookup"><span data-stu-id="40635-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="40635-457">Повторная попытка происходит незамедлительно.</span><span class="sxs-lookup"><span data-stu-id="40635-457">The retry happens immediately.</span></span> |<span data-ttu-id="40635-458">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-458">No</span></span> |<span data-ttu-id="40635-459">00:01:00 (1 минута)</span><span class="sxs-lookup"><span data-stu-id="40635-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="40635-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-460">retryTimeout</span></span> |<span data-ttu-id="40635-461">Время ожидания для каждой следующей повторной попытки.</span><span class="sxs-lookup"><span data-stu-id="40635-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="40635-462">Если это значение составляет 10 минут, проверка должна занимать не более 10 минут.</span><span class="sxs-lookup"><span data-stu-id="40635-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="40635-463">Если проверка длится больше 10 минут, возникает ошибка времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="40635-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="40635-464">Если такая ошибка возникает во время всех попыток, срез помечается как TimedOut.</span><span class="sxs-lookup"><span data-stu-id="40635-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="40635-465">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-465">No</span></span> |<span data-ttu-id="40635-466">00:10:00 (10 минут)</span><span class="sxs-lookup"><span data-stu-id="40635-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="40635-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="40635-467">maximumRetry</span></span> |<span data-ttu-id="40635-468">Максимальное количество попыток проверки доступности внешних данных.</span><span class="sxs-lookup"><span data-stu-id="40635-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="40635-469">Максимальное допустимое значение — 10.</span><span class="sxs-lookup"><span data-stu-id="40635-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="40635-470">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-470">No</span></span> |<span data-ttu-id="40635-471">3</span><span class="sxs-lookup"><span data-stu-id="40635-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="40635-472">ХРАНИЛИЩА ДАННЫХ</span><span class="sxs-lookup"><span data-stu-id="40635-472">DATA STORES</span></span>
<span data-ttu-id="40635-473">В разделе [Связанная служба](#linked-service) приводятся описания стандартных элементов JSON для всех типов связанных служб.</span><span class="sxs-lookup"><span data-stu-id="40635-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="40635-474">Этот раздел содержит сведения об элементах JSON, характерных для каждого хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="40635-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="40635-475">В разделе [Набор данных](#dataset) приводятся описания стандартных элементов JSON для всех типов наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="40635-476">Этот раздел содержит сведения об элементах JSON, характерных для каждого хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="40635-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="40635-477">В разделе [Действие](#activity) приводятся описания стандартных элементов JSON для всех типов действий.</span><span class="sxs-lookup"><span data-stu-id="40635-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="40635-478">Этот раздел содержит сведения об элементах JSON, характерных для каждого хранилища данных, когда оно используется как источник или приемник в действии копирования.</span><span class="sxs-lookup"><span data-stu-id="40635-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="40635-479">Щелкните ссылку для интересующего вас хранилища, чтобы просмотреть схемы JSON для связанной службы, набора данных, источника и приемника для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="40635-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="40635-480">Категория</span><span class="sxs-lookup"><span data-stu-id="40635-480">Category</span></span> | <span data-ttu-id="40635-481">Хранилище данных</span><span class="sxs-lookup"><span data-stu-id="40635-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="40635-482">**Таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="40635-482">**Azure**</span></span> |[<span data-ttu-id="40635-483">хранилище BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="40635-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="40635-484">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="40635-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40635-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="40635-486">База данных SQL Azure;</span><span class="sxs-lookup"><span data-stu-id="40635-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="40635-487">Хранилище данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="40635-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="40635-488">Поиск Azure;</span><span class="sxs-lookup"><span data-stu-id="40635-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="40635-489">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="40635-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="40635-490">**Базы данных**</span><span class="sxs-lookup"><span data-stu-id="40635-490">**Databases**</span></span> |[<span data-ttu-id="40635-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="40635-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="40635-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="40635-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="40635-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="40635-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="40635-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="40635-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="40635-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="40635-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="40635-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="40635-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="40635-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="40635-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="40635-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40635-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="40635-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="40635-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="40635-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="40635-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="40635-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="40635-501">**NoSQL**</span></span> |[<span data-ttu-id="40635-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="40635-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="40635-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="40635-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="40635-504">**File**</span><span class="sxs-lookup"><span data-stu-id="40635-504">**File**</span></span> |[<span data-ttu-id="40635-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="40635-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="40635-506">Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="40635-507">FTP</span><span class="sxs-lookup"><span data-stu-id="40635-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="40635-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="40635-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="40635-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="40635-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="40635-510">**Прочее**</span><span class="sxs-lookup"><span data-stu-id="40635-510">**Others**</span></span> |[<span data-ttu-id="40635-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="40635-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="40635-512">OData</span><span class="sxs-lookup"><span data-stu-id="40635-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="40635-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="40635-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="40635-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="40635-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="40635-515">Веб-таблица</span><span class="sxs-lookup"><span data-stu-id="40635-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="40635-516">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="40635-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-517">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-517">Linked service</span></span>
<span data-ttu-id="40635-518">Существует два типа связанных служб: связанная служба хранилища Azure и связанная служба SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="40635-519">Связанная служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="40635-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="40635-520">Чтобы связать учетную запись хранения Azure с фабрикой данных Azure с помощью **ключа учетной записи**, создайте связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="40635-521">Для определения связанной службы хранилища Azure задайте **AzureStorage** в качестве **типа** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="40635-522">Затем укажите следующие свойства в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="40635-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-523">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-523">Property</span></span> | <span data-ttu-id="40635-524">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-524">Description</span></span> | <span data-ttu-id="40635-525">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-526">connectionString</span></span> |<span data-ttu-id="40635-527">В свойстве connectionString указываются сведения, необходимые для подключения к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="40635-528">Да</span><span class="sxs-lookup"><span data-stu-id="40635-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="40635-529">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="40635-530">Связанная служба SAS хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="40635-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="40635-531">Связанная служба SAS хранилища Azure позволяет связать учетную запись хранения Azure с фабрикой данных Azure с помощью подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="40635-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="40635-532">В этом случае фабрика данных получает ограниченный или привязанный ко времени доступ ко всем или конкретным ресурсам (BLOB-объектам или контейнерам) в хранилище.</span><span class="sxs-lookup"><span data-stu-id="40635-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="40635-533">Чтобы связать вашу учетную запись хранения Azure с фабрикой данных с помощью подписанного URL-адреса, создайте связанную службу SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="40635-534">Для определения связанной службы SAS хранилища Azure задайте **AzureStorageSas** в качестве **типа** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="40635-535">Затем укажите следующие свойства в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="40635-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="40635-536">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-536">Property</span></span> | <span data-ttu-id="40635-537">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-537">Description</span></span> | <span data-ttu-id="40635-538">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="40635-539">sasUri</span></span> |<span data-ttu-id="40635-540">Укажите URI подписанного URL-адреса к ресурсам хранилища Azure, например BLOB-объектам, контейнерам или таблицам.</span><span class="sxs-lookup"><span data-stu-id="40635-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="40635-541">Да</span><span class="sxs-lookup"><span data-stu-id="40635-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="40635-542">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-542">Example</span></span>

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

<span data-ttu-id="40635-543">Дополнительные сведения об этих связанных службах см. в статье о [соединителе хранилища BLOB-объектов Azure](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-544">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-544">Dataset</span></span>
<span data-ttu-id="40635-545">Чтобы определить набор данных большого двоичного объекта Azure, задайте **AzureBlob** в качестве **типа** набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="40635-546">Затем укажите следующие свойства большого двоичного объекта Azure в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="40635-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-547">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-547">Property</span></span> | <span data-ttu-id="40635-548">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-548">Description</span></span> | <span data-ttu-id="40635-549">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="40635-550">folderPath</span></span> |<span data-ttu-id="40635-551">Путь контейнеру и папке в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="40635-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="40635-552">Пример: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="40635-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="40635-553">Да</span><span class="sxs-lookup"><span data-stu-id="40635-553">Yes</span></span> |
| <span data-ttu-id="40635-554">fileName</span><span class="sxs-lookup"><span data-stu-id="40635-554">fileName</span></span> |<span data-ttu-id="40635-555">Имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="40635-555">Name of the blob.</span></span> <span data-ttu-id="40635-556">Свойство fileName является необязательным и в нем учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="40635-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="40635-557">Если указать имя файла, то действие (включая копирование) работает с определенным большим двоичным объектом.</span><span class="sxs-lookup"><span data-stu-id="40635-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="40635-558">Если значение fileName не указано, то копируются все большие двоичные объекты в folderPath для входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="40635-559">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат: Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="40635-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40635-560">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-560">No</span></span> |
| <span data-ttu-id="40635-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40635-561">partitionedBy</span></span> |<span data-ttu-id="40635-562">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="40635-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="40635-563">Его можно использовать, чтобы указать динамические путь к папке и имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="40635-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="40635-564">Например, путь к папке (значение folderPath) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="40635-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="40635-565">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-565">No</span></span> |
| <span data-ttu-id="40635-566">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-566">format</span></span> | <span data-ttu-id="40635-567">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-568">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-569">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-570">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-571">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-571">No</span></span> |
| <span data-ttu-id="40635-572">compression</span><span class="sxs-lookup"><span data-stu-id="40635-572">compression</span></span> | <span data-ttu-id="40635-573">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-574">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40635-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40635-575">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-576">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-577">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-578">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-578">Example</span></span>

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


<span data-ttu-id="40635-579">Дополнительные сведения см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="40635-580">BlobSource в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="40635-581">При копировании данных из хранилища BLOB-объектов Azure задайте **BlobSource** в качестве **типа источника** для действия копирования и задайте следующие свойства в разделе **source**:</span><span class="sxs-lookup"><span data-stu-id="40635-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="40635-582">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-582">Property</span></span> | <span data-ttu-id="40635-583">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-583">Description</span></span> | <span data-ttu-id="40635-584">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-584">Allowed values</span></span> | <span data-ttu-id="40635-585">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-586">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-586">recursive</span></span> |<span data-ttu-id="40635-587">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="40635-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40635-588">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="40635-588">True (default value), False</span></span> |<span data-ttu-id="40635-589">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="40635-590">Пример: BlobSource **</span><span class="sxs-lookup"><span data-stu-id="40635-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="40635-591">BlobSink в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="40635-592">При копировании данных в хранилище BLOB-объектов Azure задайте **BlobSink** в качестве **типа приемника** для действия копирования и задайте следующие свойства в разделе **sink**:</span><span class="sxs-lookup"><span data-stu-id="40635-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-593">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-593">Property</span></span> | <span data-ttu-id="40635-594">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-594">Description</span></span> | <span data-ttu-id="40635-595">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-595">Allowed values</span></span> | <span data-ttu-id="40635-596">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="40635-597">copyBehavior</span></span> |<span data-ttu-id="40635-598">Это свойство определяет поведение функции копирования, когда в качестве источника используется BlobSource или FileSystem.</span><span class="sxs-lookup"><span data-stu-id="40635-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="40635-599"><b>PreserveHierarchy:</b> сохраняет иерархию файлов в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="40635-600">Относительный путь исходного файла в исходной папке идентичен относительному пути целевого файла в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="40635-601"><b>FlattenHierarchy</b>: все файлы из исходной папки размещаются на первом уровне в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="40635-602">Целевые файлы имеют автоматически сформированное имя.</span><span class="sxs-lookup"><span data-stu-id="40635-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="40635-603"><b>MergeFiles (по умолчанию):</b> объединяет все файлы из исходной папки в один файл.</span><span class="sxs-lookup"><span data-stu-id="40635-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="40635-604">Если указано имя файла или большого двоичного объекта, именем объединенного файла будет указанное имя; в противном случае имя файла будет автоматически сформировано.</span><span class="sxs-lookup"><span data-stu-id="40635-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="40635-605">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="40635-606">Пример: BlobSink</span><span class="sxs-lookup"><span data-stu-id="40635-606">Example: BlobSink</span></span>

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

<span data-ttu-id="40635-607">Дополнительные сведения см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="40635-608">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-609">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-609">Linked service</span></span>
<span data-ttu-id="40635-610">Для определения связанной службы Azure Data Lake Store задайте **AzureDataLakeStore** в качестве типа связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-611">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-611">Property</span></span> | <span data-ttu-id="40635-612">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-612">Description</span></span> | <span data-ttu-id="40635-613">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-614">type</span><span class="sxs-lookup"><span data-stu-id="40635-614">type</span></span> | <span data-ttu-id="40635-615">Для свойства type следует задать значение **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="40635-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="40635-616">Да</span><span class="sxs-lookup"><span data-stu-id="40635-616">Yes</span></span> |
| <span data-ttu-id="40635-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="40635-617">dataLakeStoreUri</span></span> | <span data-ttu-id="40635-618">Указывает сведения об учетной записи хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="40635-619">Используемый формат: `https://[accountname].azuredatalakestore.net/webhdfs/v1` или `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="40635-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="40635-620">Да</span><span class="sxs-lookup"><span data-stu-id="40635-620">Yes</span></span> |
| <span data-ttu-id="40635-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="40635-621">subscriptionId</span></span> | <span data-ttu-id="40635-622">Идентификатор подписки Azure, к которой принадлежит Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40635-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="40635-623">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="40635-623">Required for sink</span></span> |
| <span data-ttu-id="40635-624">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="40635-624">resourceGroupName</span></span> | <span data-ttu-id="40635-625">Имя группы ресурсов Azure, к которой принадлежит Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40635-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="40635-626">Необходимо для приемника</span><span class="sxs-lookup"><span data-stu-id="40635-626">Required for sink</span></span> |
| <span data-ttu-id="40635-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="40635-627">servicePrincipalId</span></span> | <span data-ttu-id="40635-628">Укажите идентификатора клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="40635-628">Specify the application's client ID.</span></span> | <span data-ttu-id="40635-629">Да (для проверки подлинности на основе субъекта-службы)</span><span class="sxs-lookup"><span data-stu-id="40635-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="40635-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="40635-630">servicePrincipalKey</span></span> | <span data-ttu-id="40635-631">Укажите ключ приложения.</span><span class="sxs-lookup"><span data-stu-id="40635-631">Specify the application's key.</span></span> | <span data-ttu-id="40635-632">Да (для проверки подлинности на основе субъекта-службы)</span><span class="sxs-lookup"><span data-stu-id="40635-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="40635-633">tenant</span><span class="sxs-lookup"><span data-stu-id="40635-633">tenant</span></span> | <span data-ttu-id="40635-634">Укажите сведения о клиенте (доменное имя или идентификатор клиента), в котором находится приложение.</span><span class="sxs-lookup"><span data-stu-id="40635-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="40635-635">Его можно получить, наведя указатель мыши на правый верхний угол страницы портала Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="40635-636">Да (для проверки подлинности на основе субъекта-службы)</span><span class="sxs-lookup"><span data-stu-id="40635-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="40635-637">authorization</span><span class="sxs-lookup"><span data-stu-id="40635-637">authorization</span></span> | <span data-ttu-id="40635-638">Нажмите кнопку **Авторизовать** в **редакторе фабрики данных** и введите учетные данные. URL-адрес авторизации будет создан автоматически и присвоен этому свойству.</span><span class="sxs-lookup"><span data-stu-id="40635-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="40635-639">Да (для проверки подлинности на основе учетных данных пользователя)</span><span class="sxs-lookup"><span data-stu-id="40635-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="40635-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="40635-640">sessionId</span></span> | <span data-ttu-id="40635-641">Идентификатор сеанса OAuth из сеанса авторизации OAuth.</span><span class="sxs-lookup"><span data-stu-id="40635-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="40635-642">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="40635-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="40635-643">Этот параметр создается автоматически при использовании редактора фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="40635-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="40635-644">Да (для проверки подлинности на основе учетных данных пользователя)</span><span class="sxs-lookup"><span data-stu-id="40635-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="40635-645">Пример: использование проверки подлинности на основе субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="40635-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="40635-646">Пример: использование проверки подлинности на основе учетных данных пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="40635-647">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-648">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-648">Dataset</span></span>
<span data-ttu-id="40635-649">Для определения набора данных Azure Data Lake Store задайте **AzureDataLakeStore** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-650">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-650">Property</span></span> | <span data-ttu-id="40635-651">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-651">Description</span></span> | <span data-ttu-id="40635-652">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="40635-653">folderPath</span></span> |<span data-ttu-id="40635-654">Путь к контейнеру и папке в хранилище озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="40635-655">Да</span><span class="sxs-lookup"><span data-stu-id="40635-655">Yes</span></span> |
| <span data-ttu-id="40635-656">fileName</span><span class="sxs-lookup"><span data-stu-id="40635-656">fileName</span></span> |<span data-ttu-id="40635-657">Имя файла в хранилище озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="40635-658">Свойство fileName является необязательным и в нем учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="40635-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="40635-659">Если указать имя файла, то действие (включая копирование) работает с определенным файлом.</span><span class="sxs-lookup"><span data-stu-id="40635-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="40635-660">Если значение fileName не указано, то копируются все файлы в folderPath для входного набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="40635-661">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат: Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="40635-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40635-662">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-662">No</span></span> |
| <span data-ttu-id="40635-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40635-663">partitionedBy</span></span> |<span data-ttu-id="40635-664">Необязательное свойство.</span><span class="sxs-lookup"><span data-stu-id="40635-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="40635-665">Его можно использовать, чтобы указать динамические путь к папке и имя файла для временного ряда данных.</span><span class="sxs-lookup"><span data-stu-id="40635-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="40635-666">Например, путь к папке (значение folderPath) каждый час может быть другим.</span><span class="sxs-lookup"><span data-stu-id="40635-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="40635-667">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-667">No</span></span> |
| <span data-ttu-id="40635-668">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-668">format</span></span> | <span data-ttu-id="40635-669">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-670">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-671">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-672">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-673">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-673">No</span></span> |
| <span data-ttu-id="40635-674">compression</span><span class="sxs-lookup"><span data-stu-id="40635-674">compression</span></span> | <span data-ttu-id="40635-675">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-676">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40635-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40635-677">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-678">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-679">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-680">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-680">Example</span></span>
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

<span data-ttu-id="40635-681">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="40635-682">Источник Azure Data Lake Store в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="40635-683">При копировании данных из Azure Data Lake Store задайте **AzureDataLakeStoreSource** в качестве **типа источника** для действия копирования и укажите следующие свойства в разделе **source**:</span><span class="sxs-lookup"><span data-stu-id="40635-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="40635-684">**AzureDataLakeStoreSource** поддерживает следующие свойства в разделе **typeProperties**.</span><span class="sxs-lookup"><span data-stu-id="40635-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="40635-685">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-685">Property</span></span> | <span data-ttu-id="40635-686">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-686">Description</span></span> | <span data-ttu-id="40635-687">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-687">Allowed values</span></span> | <span data-ttu-id="40635-688">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-689">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-689">recursive</span></span> |<span data-ttu-id="40635-690">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="40635-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40635-691">True (значение по умолчанию), False</span><span class="sxs-lookup"><span data-stu-id="40635-691">True (default value), False</span></span> |<span data-ttu-id="40635-692">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="40635-693">Пример: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="40635-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="40635-694">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="40635-695">Приемник Azure Data Lake Store в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="40635-696">При копировании данных в Azure Data Lake Store задайте **AzureDataLakeStoreSink** в качестве **типа приемника** для действия копирования и укажите следующие свойства в разделе **sink**:</span><span class="sxs-lookup"><span data-stu-id="40635-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-697">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-697">Property</span></span> | <span data-ttu-id="40635-698">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-698">Description</span></span> | <span data-ttu-id="40635-699">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-699">Allowed values</span></span> | <span data-ttu-id="40635-700">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="40635-701">copyBehavior</span></span> |<span data-ttu-id="40635-702">Определяет поведение копирования.</span><span class="sxs-lookup"><span data-stu-id="40635-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="40635-703"><b>PreserveHierarchy:</b> сохраняет иерархию файлов в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="40635-704">Относительный путь исходного файла в исходной папке идентичен относительному пути целевого файла в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="40635-705"><b>FlattenHierarchy</b>: все файлы из исходной папки создаются на первом уровне в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="40635-706">Целевые файлы создаются с автоматически создаваемыми именами.</span><span class="sxs-lookup"><span data-stu-id="40635-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="40635-707"><b>MergeFiles</b>: объединяет все файлы из исходной папки в один файл.</span><span class="sxs-lookup"><span data-stu-id="40635-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="40635-708">Если указано имя файла или большого двоичного объекта, именем объединенного файла будет указанное имя; в противном случае имя файла будет автоматически сформировано.</span><span class="sxs-lookup"><span data-stu-id="40635-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="40635-709">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="40635-710">Пример: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="40635-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="40635-711">Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="40635-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="40635-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="40635-713">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-713">Linked service</span></span>
<span data-ttu-id="40635-714">Для определения связанной службы Azure Cosmos DB задайте **DocumentDb** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-715">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="40635-715">**Property**</span></span> | <span data-ttu-id="40635-716">**Описание**</span><span class="sxs-lookup"><span data-stu-id="40635-716">**Description**</span></span> | <span data-ttu-id="40635-717">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="40635-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-718">connectionString</span></span> |<span data-ttu-id="40635-719">Укажите сведения, необходимые для подключения к базе данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40635-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="40635-720">Да</span><span class="sxs-lookup"><span data-stu-id="40635-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-721">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-721">Example</span></span>

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
<span data-ttu-id="40635-722">Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-723">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-723">Dataset</span></span>
<span data-ttu-id="40635-724">Для определения набора данных Azure Cosmos DB задайте **DocumentDbCollection** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-725">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="40635-725">**Property**</span></span> | <span data-ttu-id="40635-726">**Описание**</span><span class="sxs-lookup"><span data-stu-id="40635-726">**Description**</span></span> | <span data-ttu-id="40635-727">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="40635-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="40635-728">collectionName</span></span> |<span data-ttu-id="40635-729">Имя коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40635-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="40635-730">Да</span><span class="sxs-lookup"><span data-stu-id="40635-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-731">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-731">Example</span></span>

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
<span data-ttu-id="40635-732">Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="40635-733">Источник коллекции Azure Cosmos DB в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="40635-734">При копировании данных из Azure Cosmos DB задайте **DocumentDbCollectionSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-735">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="40635-735">**Property**</span></span> | <span data-ttu-id="40635-736">**Описание**</span><span class="sxs-lookup"><span data-stu-id="40635-736">**Description**</span></span> | <span data-ttu-id="40635-737">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="40635-737">**Allowed values**</span></span> | <span data-ttu-id="40635-738">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="40635-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-739">запрос</span><span class="sxs-lookup"><span data-stu-id="40635-739">query</span></span> |<span data-ttu-id="40635-740">Запрос, нужный для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-740">Specify the query to read data.</span></span> |<span data-ttu-id="40635-741">Строка запроса, поддерживаемая Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="40635-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="40635-742">Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="40635-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="40635-743">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-743">No</span></span> <br/><br/><span data-ttu-id="40635-744">Если не указано, то выполняется инструкция SQL `select <columns defined in structure> from mycollection`.</span><span class="sxs-lookup"><span data-stu-id="40635-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="40635-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="40635-745">nestingSeparator</span></span> |<span data-ttu-id="40635-746">Специальный символ, обозначающий, что документ является вложенным.</span><span class="sxs-lookup"><span data-stu-id="40635-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="40635-747">Любой символ.</span><span class="sxs-lookup"><span data-stu-id="40635-747">Any character.</span></span> <br/><br/><span data-ttu-id="40635-748">Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры.</span><span class="sxs-lookup"><span data-stu-id="40635-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="40635-749">Фабрика данных Azure позволяет обозначать иерархию с помощью разделителя nestingSeparator.</span><span class="sxs-lookup"><span data-stu-id="40635-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="40635-750">В приведенных выше примерах это точка.</span><span class="sxs-lookup"><span data-stu-id="40635-750">in the above examples.</span></span> <span data-ttu-id="40635-751">Благодаря этому разделителю действие копирование создаст объект Name с тремя дочерними элементами, First, Middle и Last, в соответствии с элементами Name.First, Name.Middle и Name.Last в определении таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="40635-752">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-753">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="40635-754">Приемник коллекции Azure Cosmos DB в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="40635-755">При копировании данных в Azure Cosmos DB задайте **DocumentDbCollectionSink** в качестве **типа приемника** для действия копирования и укажите в разделе **sink** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-756">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="40635-756">**Property**</span></span> | <span data-ttu-id="40635-757">**Описание**</span><span class="sxs-lookup"><span data-stu-id="40635-757">**Description**</span></span> | <span data-ttu-id="40635-758">**Допустимые значения**</span><span class="sxs-lookup"><span data-stu-id="40635-758">**Allowed values**</span></span> | <span data-ttu-id="40635-759">**Обязательный**</span><span class="sxs-lookup"><span data-stu-id="40635-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="40635-760">nestingSeparator</span></span> |<span data-ttu-id="40635-761">Такой специальный символ в имени исходного столбца, который указывает, что нужен вложенный документ.</span><span class="sxs-lookup"><span data-stu-id="40635-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="40635-762">См. пример выше: элемент `Name.First` в выходной таблице обуславливает в документе Cosmos DB такую структуру JSON:</span><span class="sxs-lookup"><span data-stu-id="40635-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="40635-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="40635-763">"Name": {</span></span><br/>    <span data-ttu-id="40635-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="40635-764">"First": "John"</span></span><br/><span data-ttu-id="40635-765">},</span><span class="sxs-lookup"><span data-stu-id="40635-765">},</span></span> |<span data-ttu-id="40635-766">Символ, используемый для разделения уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="40635-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="40635-767">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="40635-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="40635-768">Символ, используемый для разделения уровней вложенности.</span><span class="sxs-lookup"><span data-stu-id="40635-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="40635-769">Значение по умолчанию — `.` (точка).</span><span class="sxs-lookup"><span data-stu-id="40635-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="40635-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-770">writeBatchSize</span></span> |<span data-ttu-id="40635-771">Число параллельных запросов к службе Azure Cosmos DB для создания документов.</span><span class="sxs-lookup"><span data-stu-id="40635-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="40635-772">При копировании данных из или в Azure Cosmos DB с помощью этого свойства можно оптимизировать производительность.</span><span class="sxs-lookup"><span data-stu-id="40635-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="40635-773">Если увеличить значение свойства writeBatchSize, то производительность повышается, потому что в Azure Cosmos DB начинает поступать больше параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="40635-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="40635-774">Однако необходимо избежать регулирования, которое может вызвать сообщение об ошибке: "Высокая частота запросов".</span><span class="sxs-lookup"><span data-stu-id="40635-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="40635-775">Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования вы можете использовать коллекцию получше (например, S3), чтобы обеспечить максимальную пропускную способность (2500 единиц запроса в секунду).</span><span class="sxs-lookup"><span data-stu-id="40635-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="40635-776">Число</span><span class="sxs-lookup"><span data-stu-id="40635-776">Integer</span></span> |<span data-ttu-id="40635-777">Нет (значение по умолчанию — 5)</span><span class="sxs-lookup"><span data-stu-id="40635-777">No (default: 5)</span></span> |
| <span data-ttu-id="40635-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-778">writeBatchTimeout</span></span> |<span data-ttu-id="40635-779">Время ожидания до выполнения операции, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="40635-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="40635-780">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="40635-780">timespan</span></span><br/><br/> <span data-ttu-id="40635-781">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40635-782">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-783">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
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

<span data-ttu-id="40635-784">Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="40635-785">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-786">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-786">Linked service</span></span>
<span data-ttu-id="40635-787">Для определения связанной службы базы данных SQL Azure задайте **AzureSqlDatabase** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-788">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-788">Property</span></span> | <span data-ttu-id="40635-789">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-789">Description</span></span> | <span data-ttu-id="40635-790">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-791">connectionString</span></span> |<span data-ttu-id="40635-792">В свойстве connectionString указываются сведения, необходимые для подключения к экземпляру базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="40635-793">Да</span><span class="sxs-lookup"><span data-stu-id="40635-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-794">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-794">Example</span></span>
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

<span data-ttu-id="40635-795">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-796">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-796">Dataset</span></span>
<span data-ttu-id="40635-797">Для определения набора данных базы данных SQL Azure задайте **AzureSqlTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-798">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-798">Property</span></span> | <span data-ttu-id="40635-799">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-799">Description</span></span> | <span data-ttu-id="40635-800">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-801">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-801">tableName</span></span> |<span data-ttu-id="40635-802">Имя таблицы или представления в экземпляре базы данных SQL Azure, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="40635-803">Да</span><span class="sxs-lookup"><span data-stu-id="40635-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-804">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-804">Example</span></span>

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
<span data-ttu-id="40635-805">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="40635-806">Источник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="40635-807">При копировании данных из базы данных SQL Azure задайте **SqlSource** в качестве **типа источника** для действия копирования и задайте в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-808">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-808">Property</span></span> | <span data-ttu-id="40635-809">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-809">Description</span></span> | <span data-ttu-id="40635-810">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-810">Allowed values</span></span> | <span data-ttu-id="40635-811">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40635-812">sqlReaderQuery</span></span> |<span data-ttu-id="40635-813">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-813">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-814">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-814">SQL query string.</span></span> <span data-ttu-id="40635-815">Пример: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-816">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-816">No</span></span> |
| <span data-ttu-id="40635-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40635-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="40635-818">Имя хранимой процедуры, которая считывает данные из исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="40635-819">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-819">Name of the stored procedure.</span></span> |<span data-ttu-id="40635-820">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-820">No</span></span> |
| <span data-ttu-id="40635-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40635-821">storedProcedureParameters</span></span> |<span data-ttu-id="40635-822">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40635-823">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="40635-823">Name/value pairs.</span></span> <span data-ttu-id="40635-824">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40635-825">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-826">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-826">Example</span></span>

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
<span data-ttu-id="40635-827">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="40635-828">Приемник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="40635-829">При копировании данных в базу данных SQL Azure задайте **SqlSink** в качестве **типа приемника** для действия копирования и задайте в разделе **sink** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-830">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-830">Property</span></span> | <span data-ttu-id="40635-831">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-831">Description</span></span> | <span data-ttu-id="40635-832">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-832">Allowed values</span></span> | <span data-ttu-id="40635-833">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-834">writeBatchTimeout</span></span> |<span data-ttu-id="40635-835">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="40635-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40635-836">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="40635-836">timespan</span></span><br/><br/> <span data-ttu-id="40635-837">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40635-838">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-838">No</span></span> |
| <span data-ttu-id="40635-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-839">writeBatchSize</span></span> |<span data-ttu-id="40635-840">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="40635-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="40635-841">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="40635-841">Integer (number of rows)</span></span> |<span data-ttu-id="40635-842">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="40635-842">No (default: 10000)</span></span> |
| <span data-ttu-id="40635-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40635-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40635-844">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="40635-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="40635-845">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-845">A query statement.</span></span> |<span data-ttu-id="40635-846">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-846">No</span></span> |
| <span data-ttu-id="40635-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="40635-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="40635-848">Укажите имя столбца, в которое действие копирования добавляет автоматически созданный идентификатор среза. Этот идентификатор используется для очистки данных конкретного среза при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="40635-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="40635-849">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="40635-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="40635-850">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-850">No</span></span> |
| <span data-ttu-id="40635-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40635-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="40635-852">Имя хранимой процедуры, обновляющей данные или вставляющей их в целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="40635-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="40635-853">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-853">Name of the stored procedure.</span></span> |<span data-ttu-id="40635-854">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-854">No</span></span> |
| <span data-ttu-id="40635-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40635-855">storedProcedureParameters</span></span> |<span data-ttu-id="40635-856">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40635-857">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="40635-857">Name/value pairs.</span></span> <span data-ttu-id="40635-858">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40635-859">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-859">No</span></span> |
| <span data-ttu-id="40635-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="40635-860">sqlWriterTableType</span></span> |<span data-ttu-id="40635-861">Укажите имя типа таблицы для использования в хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="40635-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="40635-862">Действие копирования делает перемещаемые данные доступными во временной таблице этого типа.</span><span class="sxs-lookup"><span data-stu-id="40635-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="40635-863">Код хранимой процедуры затем можно использовать для объединения копируемых и существующих данных.</span><span class="sxs-lookup"><span data-stu-id="40635-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="40635-864">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-864">A table type name.</span></span> |<span data-ttu-id="40635-865">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-866">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-866">Example</span></span>

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

<span data-ttu-id="40635-867">Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="40635-868">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-869">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-869">Linked service</span></span>
<span data-ttu-id="40635-870">Для определения связанной службы хранилища данных SQL Azure задайте **AzureSqlDW** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-871">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-871">Property</span></span> | <span data-ttu-id="40635-872">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-872">Description</span></span> | <span data-ttu-id="40635-873">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-874">connectionString</span></span> |<span data-ttu-id="40635-875">Укажите сведения, необходимые для подключения к экземпляру хранилища данных SQL Azure, для свойства connectionString.</span><span class="sxs-lookup"><span data-stu-id="40635-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="40635-876">Да</span><span class="sxs-lookup"><span data-stu-id="40635-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="40635-877">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-877">Example</span></span>

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

<span data-ttu-id="40635-878">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-879">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-879">Dataset</span></span>
<span data-ttu-id="40635-880">Для определения набора данных хранилища данных SQL Azure задайте **AzureSqlDWTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-881">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-881">Property</span></span> | <span data-ttu-id="40635-882">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-882">Description</span></span> | <span data-ttu-id="40635-883">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-884">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-884">tableName</span></span> |<span data-ttu-id="40635-885">Имя таблицы или представления в базе данных хранилища данных SQL Azure, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="40635-886">Да</span><span class="sxs-lookup"><span data-stu-id="40635-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-887">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-887">Example</span></span>

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

<span data-ttu-id="40635-888">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="40635-889">Источник хранилища данных SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="40635-890">При копировании данных из хранилища данных SQL Azure задайте **SqlDWSource** в качестве **типа источника** для действия копирования и задайте в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-891">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-891">Property</span></span> | <span data-ttu-id="40635-892">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-892">Description</span></span> | <span data-ttu-id="40635-893">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-893">Allowed values</span></span> | <span data-ttu-id="40635-894">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40635-895">sqlReaderQuery</span></span> |<span data-ttu-id="40635-896">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-896">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-897">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-897">SQL query string.</span></span> <span data-ttu-id="40635-898">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-899">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-899">No</span></span> |
| <span data-ttu-id="40635-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40635-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="40635-901">Имя хранимой процедуры, которая считывает данные из исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="40635-902">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-902">Name of the stored procedure.</span></span> |<span data-ttu-id="40635-903">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-903">No</span></span> |
| <span data-ttu-id="40635-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40635-904">storedProcedureParameters</span></span> |<span data-ttu-id="40635-905">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40635-906">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="40635-906">Name/value pairs.</span></span> <span data-ttu-id="40635-907">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40635-908">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-909">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-909">Example</span></span>

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

<span data-ttu-id="40635-910">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="40635-911">Приемник хранилища данных SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="40635-912">При копировании данных в хранилище данных SQL Azure задайте **SqlDWSink** в качестве **типа приемника** для действия копирования и укажите в разделе **sink** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-913">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-913">Property</span></span> | <span data-ttu-id="40635-914">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-914">Description</span></span> | <span data-ttu-id="40635-915">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-915">Allowed values</span></span> | <span data-ttu-id="40635-916">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40635-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40635-918">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="40635-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="40635-919">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-919">A query statement.</span></span> |<span data-ttu-id="40635-920">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-920">No</span></span> |
| <span data-ttu-id="40635-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="40635-921">allowPolyBase</span></span> |<span data-ttu-id="40635-922">Указывает, следует ли использовать PolyBase (если применимо) вместо механизма BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="40635-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="40635-923">**Использование PolyBase — рекомендуемый способ загрузки данных в хранилище данных SQL.**</span><span class="sxs-lookup"><span data-stu-id="40635-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="40635-924">Да</span><span class="sxs-lookup"><span data-stu-id="40635-924">True</span></span> <br/><span data-ttu-id="40635-925">False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-925">False (default)</span></span> |<span data-ttu-id="40635-926">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-926">No</span></span> |
| <span data-ttu-id="40635-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="40635-927">polyBaseSettings</span></span> |<span data-ttu-id="40635-928">Группа свойств, которые можно задать, если свойство **allowPolybase** имеет значение **true**.</span><span class="sxs-lookup"><span data-stu-id="40635-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="40635-929">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-929">No</span></span> |
| <span data-ttu-id="40635-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="40635-930">rejectValue</span></span> |<span data-ttu-id="40635-931">Указывает количество или процент строк, которые могут быть отклонены, прежде чем запрос завершится с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="40635-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="40635-932">Дополнительные сведения о параметрах отклонения PolyBase см. в подразделе **Аргументы** раздела [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx).</span><span class="sxs-lookup"><span data-stu-id="40635-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="40635-933">0 (по умолчанию), 1, 2, ...</span><span class="sxs-lookup"><span data-stu-id="40635-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="40635-934">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-934">No</span></span> |
| <span data-ttu-id="40635-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="40635-935">rejectType</span></span> |<span data-ttu-id="40635-936">Указывает тип значения, заданного для параметра rejectValue: литеральное значение или процент.</span><span class="sxs-lookup"><span data-stu-id="40635-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="40635-937">Value (по умолчанию), Percentage</span><span class="sxs-lookup"><span data-stu-id="40635-937">Value (default), Percentage</span></span> |<span data-ttu-id="40635-938">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-938">No</span></span> |
| <span data-ttu-id="40635-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="40635-939">rejectSampleValue</span></span> |<span data-ttu-id="40635-940">Определяет количество строк, которое PolyBase следует получить до повторного вычисления процента отклоненных строк.</span><span class="sxs-lookup"><span data-stu-id="40635-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="40635-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="40635-941">1, 2, …</span></span> |<span data-ttu-id="40635-942">Да, если **rejectType** имеет значение **percentage**.</span><span class="sxs-lookup"><span data-stu-id="40635-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="40635-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="40635-943">useTypeDefault</span></span> |<span data-ttu-id="40635-944">Указывает способ обработки отсутствующих значений в текстовых файлах с разделителями, когда PolyBase получает данные из текстового файла.</span><span class="sxs-lookup"><span data-stu-id="40635-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="40635-945">Дополнительные сведения об этом свойстве см. в подразделе "Аргументы" раздела [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="40635-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="40635-946">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-946">True, False (default)</span></span> |<span data-ttu-id="40635-947">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-947">No</span></span> |
| <span data-ttu-id="40635-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-948">writeBatchSize</span></span> |<span data-ttu-id="40635-949">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="40635-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="40635-950">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="40635-950">Integer (number of rows)</span></span> |<span data-ttu-id="40635-951">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="40635-951">No (default: 10000)</span></span> |
| <span data-ttu-id="40635-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-952">writeBatchTimeout</span></span> |<span data-ttu-id="40635-953">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="40635-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40635-954">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="40635-954">timespan</span></span><br/><br/> <span data-ttu-id="40635-955">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40635-956">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-957">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-957">Example</span></span>

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

<span data-ttu-id="40635-958">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="40635-959">поиск Azure;</span><span class="sxs-lookup"><span data-stu-id="40635-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-960">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-960">Linked service</span></span>
<span data-ttu-id="40635-961">Для определения связанной службы Поиска Azure задайте **AzureSearch** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-962">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-962">Property</span></span> | <span data-ttu-id="40635-963">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-963">Description</span></span> | <span data-ttu-id="40635-964">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40635-965">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="40635-965">url</span></span> | <span data-ttu-id="40635-966">URL-адрес службы Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="40635-967">Да</span><span class="sxs-lookup"><span data-stu-id="40635-967">Yes</span></span> |
| <span data-ttu-id="40635-968">key</span><span class="sxs-lookup"><span data-stu-id="40635-968">key</span></span> | <span data-ttu-id="40635-969">Ключ администратора службы Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="40635-970">Да</span><span class="sxs-lookup"><span data-stu-id="40635-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-971">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-971">Example</span></span>

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

<span data-ttu-id="40635-972">Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-973">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-973">Dataset</span></span>
<span data-ttu-id="40635-974">Для определения набора данных Поиска Azure задайте **AzureSearchIndex** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-975">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-975">Property</span></span> | <span data-ttu-id="40635-976">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-976">Description</span></span> | <span data-ttu-id="40635-977">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40635-978">type</span><span class="sxs-lookup"><span data-stu-id="40635-978">type</span></span> | <span data-ttu-id="40635-979">Для свойства type необходимо задать значение **AzureSearchIndex**</span><span class="sxs-lookup"><span data-stu-id="40635-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="40635-980">Да</span><span class="sxs-lookup"><span data-stu-id="40635-980">Yes</span></span> |
| <span data-ttu-id="40635-981">indexName</span><span class="sxs-lookup"><span data-stu-id="40635-981">indexName</span></span> | <span data-ttu-id="40635-982">Имя индекса Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-982">Name of the Azure Search index.</span></span> <span data-ttu-id="40635-983">Фабрика данных не создает индекс.</span><span class="sxs-lookup"><span data-stu-id="40635-983">Data Factory does not create the index.</span></span> <span data-ttu-id="40635-984">Индекс должен существовать в Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="40635-985">Да</span><span class="sxs-lookup"><span data-stu-id="40635-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-986">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-986">Example</span></span>

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

<span data-ttu-id="40635-987">Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="40635-988">Приемник индекса Поиска Azure в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="40635-989">При копировании данных в индекс Поиска Azure задайте **AzureSearchIndexSink** в качестве **типа приемника** для действия копирования и укажите в разделе **sink** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-990">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-990">Property</span></span> | <span data-ttu-id="40635-991">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-991">Description</span></span> | <span data-ttu-id="40635-992">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-992">Allowed values</span></span> | <span data-ttu-id="40635-993">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="40635-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="40635-994">WriteBehavior</span></span> | <span data-ttu-id="40635-995">Указывает действие (объединение или замена), выполняемое, если документ уже существует в индексе.</span><span class="sxs-lookup"><span data-stu-id="40635-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="40635-996">Merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-996">Merge (default)</span></span><br/><span data-ttu-id="40635-997">Отправить</span><span class="sxs-lookup"><span data-stu-id="40635-997">Upload</span></span>| <span data-ttu-id="40635-998">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-998">No</span></span> |
| <span data-ttu-id="40635-999">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-999">WriteBatchSize</span></span> | <span data-ttu-id="40635-1000">Передает данные в индекс Поиска Azure, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="40635-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="40635-1001">1–1000.</span><span class="sxs-lookup"><span data-stu-id="40635-1001">1 to 1,000.</span></span> <span data-ttu-id="40635-1002">Значение по умолчанию — 1000.</span><span class="sxs-lookup"><span data-stu-id="40635-1002">Default value is 1000.</span></span> | <span data-ttu-id="40635-1003">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1004">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1004">Example</span></span>

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

<span data-ttu-id="40635-1005">Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="40635-1006">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="40635-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1007">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1007">Linked service</span></span>
<span data-ttu-id="40635-1008">Существует два типа связанных служб: связанная служба хранилища Azure и связанная служба SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="40635-1009">Связанная служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="40635-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="40635-1010">Чтобы связать учетную запись хранения Azure с фабрикой данных Azure с помощью **ключа учетной записи**, создайте связанную службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="40635-1011">Для определения связанной службы хранилища Azure задайте **AzureStorage** в качестве **типа** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="40635-1012">Затем укажите следующие свойства в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="40635-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1013">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1013">Property</span></span> | <span data-ttu-id="40635-1014">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1014">Description</span></span> | <span data-ttu-id="40635-1015">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-1016">type</span><span class="sxs-lookup"><span data-stu-id="40635-1016">type</span></span> |<span data-ttu-id="40635-1017">Для свойства type необходимо задать значение **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="40635-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="40635-1018">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1018">Yes</span></span> |
| <span data-ttu-id="40635-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-1019">connectionString</span></span> |<span data-ttu-id="40635-1020">В свойстве connectionString указываются сведения, необходимые для подключения к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="40635-1021">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1021">Yes</span></span> |

<span data-ttu-id="40635-1022">**Пример**</span><span class="sxs-lookup"><span data-stu-id="40635-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="40635-1023">Связанная служба SAS хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="40635-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="40635-1024">Связанная служба SAS хранилища Azure позволяет связать учетную запись хранения Azure с фабрикой данных Azure с помощью подписанного URL-адреса (SAS).</span><span class="sxs-lookup"><span data-stu-id="40635-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="40635-1025">В этом случае фабрика данных получает ограниченный или привязанный ко времени доступ ко всем или конкретным ресурсам (BLOB-объектам или контейнерам) в хранилище.</span><span class="sxs-lookup"><span data-stu-id="40635-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="40635-1026">Чтобы связать вашу учетную запись хранения Azure с фабрикой данных с помощью подписанного URL-адреса, создайте связанную службу SAS хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="40635-1027">Для определения связанной службы SAS хранилища Azure задайте **AzureStorageSas** в качестве **типа** связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="40635-1028">Затем укажите следующие свойства в разделе **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="40635-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="40635-1029">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1029">Property</span></span> | <span data-ttu-id="40635-1030">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1030">Description</span></span> | <span data-ttu-id="40635-1031">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-1032">type</span><span class="sxs-lookup"><span data-stu-id="40635-1032">type</span></span> |<span data-ttu-id="40635-1033">Для свойства type необходимо задать значение **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="40635-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="40635-1034">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1034">Yes</span></span> |
| <span data-ttu-id="40635-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="40635-1035">sasUri</span></span> |<span data-ttu-id="40635-1036">Укажите URI подписанного URL-адреса к ресурсам хранилища Azure, например BLOB-объектам, контейнерам или таблицам.</span><span class="sxs-lookup"><span data-stu-id="40635-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="40635-1037">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1037">Yes</span></span> |

<span data-ttu-id="40635-1038">**Пример**</span><span class="sxs-lookup"><span data-stu-id="40635-1038">**Example:**</span></span>

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

<span data-ttu-id="40635-1039">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1040">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1040">Dataset</span></span>
<span data-ttu-id="40635-1041">Для определения набора данных таблицы Azure задайте **AzureTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1042">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1042">Property</span></span> | <span data-ttu-id="40635-1043">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1043">Description</span></span> | <span data-ttu-id="40635-1044">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1045">tableName</span></span> |<span data-ttu-id="40635-1046">Имя таблицы в экземпляре базы данных таблиц Azure, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="40635-1047">Да.</span><span class="sxs-lookup"><span data-stu-id="40635-1047">Yes.</span></span> <span data-ttu-id="40635-1048">Если tableName указывается без azureTableSourceQuery, все записи из таблицы копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="40635-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="40635-1049">Если azureTableSourceQuery указывается, записи из таблицы, удовлетворяющие запросу, копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="40635-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1050">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1050">Example</span></span>

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

<span data-ttu-id="40635-1051">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="40635-1052">Источник таблицы Azure в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="40635-1053">При копировании данных из Хранилища таблиц Azure задайте **AzureTableSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1054">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1054">Property</span></span> | <span data-ttu-id="40635-1055">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1055">Description</span></span> | <span data-ttu-id="40635-1056">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1056">Allowed values</span></span> | <span data-ttu-id="40635-1057">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="40635-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="40635-1059">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1060">Строка запроса таблицы Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-1060">Azure table query string.</span></span> <span data-ttu-id="40635-1061">Примеры приведены в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="40635-1061">See examples in the next section.</span></span> |<span data-ttu-id="40635-1062">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-1062">No.</span></span> <span data-ttu-id="40635-1063">Если tableName указывается без azureTableSourceQuery, все записи из таблицы копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="40635-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="40635-1064">Если azureTableSourceQuery указывается, записи из таблицы, удовлетворяющие запросу, копируются в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="40635-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="40635-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="40635-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="40635-1066">Указывает, игнорируются ли исключения таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="40635-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="40635-1067">TRUE</span></span><br/><span data-ttu-id="40635-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="40635-1068">FALSE</span></span> |<span data-ttu-id="40635-1069">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1070">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1070">Example</span></span>

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

<span data-ttu-id="40635-1071">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="40635-1072">Приемник таблицы Azure в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="40635-1073">При копировании данных в Хранилище таблиц Azure задайте **AzureTableSink** в качестве **типа приемника** для действия копирования и задайте следующие свойства в разделе **sink**:</span><span class="sxs-lookup"><span data-stu-id="40635-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-1074">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1074">Property</span></span> | <span data-ttu-id="40635-1075">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1075">Description</span></span> | <span data-ttu-id="40635-1076">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1076">Allowed values</span></span> | <span data-ttu-id="40635-1077">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="40635-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="40635-1079">Значение ключа раздела по умолчанию, которое может использоваться приемником.</span><span class="sxs-lookup"><span data-stu-id="40635-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="40635-1080">Строковое значение.</span><span class="sxs-lookup"><span data-stu-id="40635-1080">A string value.</span></span> |<span data-ttu-id="40635-1081">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1081">No</span></span> |
| <span data-ttu-id="40635-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="40635-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="40635-1083">Укажите имя столбца, значения которого используются в качестве ключей секций.</span><span class="sxs-lookup"><span data-stu-id="40635-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="40635-1084">Если не указано, в качестве ключа раздела используется AzureTableDefaultPartitionKeyValue.</span><span class="sxs-lookup"><span data-stu-id="40635-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="40635-1085">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="40635-1085">A column name.</span></span> |<span data-ttu-id="40635-1086">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1086">No</span></span> |
| <span data-ttu-id="40635-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="40635-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="40635-1088">Укажите имя столбца, значения которого используются в качестве ключа строки.</span><span class="sxs-lookup"><span data-stu-id="40635-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="40635-1089">Если имя не указано, используйте для каждой строки идентификатор GUID.</span><span class="sxs-lookup"><span data-stu-id="40635-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="40635-1090">Имя столбца.</span><span class="sxs-lookup"><span data-stu-id="40635-1090">A column name.</span></span> |<span data-ttu-id="40635-1091">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1091">No</span></span> |
| <span data-ttu-id="40635-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="40635-1092">azureTableInsertType</span></span> |<span data-ttu-id="40635-1093">Режим для вставки данных в таблицу Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="40635-1094">Это свойство контролирует, будут ли заменены или объединены значения в существующих строках в выходной таблице с совпадающими ключами секций и строк.</span><span class="sxs-lookup"><span data-stu-id="40635-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="40635-1095">Чтобы узнать о действии этих параметров (merge и replace), ознакомьтесь со статьями [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) (Вставка или слияние сущностей) и [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) (Вставка или замена сущности).</span><span class="sxs-lookup"><span data-stu-id="40635-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="40635-1096">Этот параметр применяется на уровне строки, а не таблицы, и ни один из параметров не приводит к удалению строк в выходной таблице, которые отсутствуют во входных данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="40635-1097">merge (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-1097">merge (default)</span></span><br/><span data-ttu-id="40635-1098">replace</span><span class="sxs-lookup"><span data-stu-id="40635-1098">replace</span></span> |<span data-ttu-id="40635-1099">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1099">No</span></span> |
| <span data-ttu-id="40635-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-1100">writeBatchSize</span></span> |<span data-ttu-id="40635-1101">Вставка данных в таблицу Azure при достижении writeBatchSize или writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="40635-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="40635-1102">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="40635-1102">Integer (number of rows)</span></span> |<span data-ttu-id="40635-1103">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="40635-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="40635-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-1104">writeBatchTimeout</span></span> |<span data-ttu-id="40635-1105">Вставка данных в таблицу Azure при достижении writeBatchSize или writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="40635-1106">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="40635-1106">timespan</span></span><br/><br/><span data-ttu-id="40635-1107">Пример: 00:20:00 (20 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="40635-1108">Нет (по умолчанию используется время ожидания, стандартное для клиента хранения — 90 секунд)</span><span class="sxs-lookup"><span data-stu-id="40635-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1109">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1109">Example</span></span>

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
<span data-ttu-id="40635-1110">Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="40635-1111">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="40635-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1112">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1112">Linked service</span></span>
<span data-ttu-id="40635-1113">Для определения связанной службы Amazon Redshift задайте **AmazonRedshift** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1114">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1114">Property</span></span> | <span data-ttu-id="40635-1115">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1115">Description</span></span> | <span data-ttu-id="40635-1116">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1117">server</span><span class="sxs-lookup"><span data-stu-id="40635-1117">server</span></span> |<span data-ttu-id="40635-1118">IP-адрес или имя узла сервера Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="40635-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="40635-1119">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1119">Yes</span></span> |
| <span data-ttu-id="40635-1120">порт</span><span class="sxs-lookup"><span data-stu-id="40635-1120">port</span></span> |<span data-ttu-id="40635-1121">Номер TCP-порта, используемого сервером Amazon Redshift для прослушивания клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="40635-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="40635-1122">Нет, значение по умолчанию — 5439.</span><span class="sxs-lookup"><span data-stu-id="40635-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="40635-1123">database</span><span class="sxs-lookup"><span data-stu-id="40635-1123">database</span></span> |<span data-ttu-id="40635-1124">Имя базы данных Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="40635-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="40635-1125">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1125">Yes</span></span> |
| <span data-ttu-id="40635-1126">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1126">username</span></span> |<span data-ttu-id="40635-1127">Имя пользователя, имеющего доступ к базе данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="40635-1128">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1128">Yes</span></span> |
| <span data-ttu-id="40635-1129">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1129">password</span></span> |<span data-ttu-id="40635-1130">Пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1130">Password for the user account.</span></span> |<span data-ttu-id="40635-1131">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1132">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1132">Example</span></span>

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

<span data-ttu-id="40635-1133">Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1134">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1134">Dataset</span></span>
<span data-ttu-id="40635-1135">Для определения набора данных Amazon Redshift задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1136">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1136">Property</span></span> | <span data-ttu-id="40635-1137">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1137">Description</span></span> | <span data-ttu-id="40635-1138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1139">tableName</span></span> |<span data-ttu-id="40635-1140">Имя таблицы в базе данных Amazon Redshift, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="40635-1141">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="40635-1142">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1142">Example</span></span>

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
<span data-ttu-id="40635-1143">Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1144">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="40635-1145">При копировании данных из Amazon Redshift задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1146">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1146">Property</span></span> | <span data-ttu-id="40635-1147">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1147">Description</span></span> | <span data-ttu-id="40635-1148">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1148">Allowed values</span></span> | <span data-ttu-id="40635-1149">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1150">query</span><span class="sxs-lookup"><span data-stu-id="40635-1150">query</span></span> |<span data-ttu-id="40635-1151">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1152">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1152">SQL query string.</span></span> <span data-ttu-id="40635-1153">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-1154">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1155">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1155">Example</span></span>

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
<span data-ttu-id="40635-1156">Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="40635-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="40635-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1158">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1158">Linked service</span></span>
<span data-ttu-id="40635-1159">Для определения связанной службы IBM DB2 задайте **OnPremisesDB2** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1160">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1160">Property</span></span> | <span data-ttu-id="40635-1161">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1161">Description</span></span> | <span data-ttu-id="40635-1162">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1163">server</span><span class="sxs-lookup"><span data-stu-id="40635-1163">server</span></span> |<span data-ttu-id="40635-1164">Имя сервера DB2.</span><span class="sxs-lookup"><span data-stu-id="40635-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="40635-1165">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1165">Yes</span></span> |
| <span data-ttu-id="40635-1166">database</span><span class="sxs-lookup"><span data-stu-id="40635-1166">database</span></span> |<span data-ttu-id="40635-1167">Имя базы данных DB2.</span><span class="sxs-lookup"><span data-stu-id="40635-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="40635-1168">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1168">Yes</span></span> |
| <span data-ttu-id="40635-1169">schema</span><span class="sxs-lookup"><span data-stu-id="40635-1169">schema</span></span> |<span data-ttu-id="40635-1170">Имя схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1170">Name of the schema in the database.</span></span> <span data-ttu-id="40635-1171">Имя схемы чувствительно к регистру.</span><span class="sxs-lookup"><span data-stu-id="40635-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="40635-1172">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1172">No</span></span> |
| <span data-ttu-id="40635-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1173">authenticationType</span></span> |<span data-ttu-id="40635-1174">Тип проверки подлинности, используемый для подключения к базе данных DB2.</span><span class="sxs-lookup"><span data-stu-id="40635-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="40635-1175">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40635-1176">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1176">Yes</span></span> |
| <span data-ttu-id="40635-1177">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1177">username</span></span> |<span data-ttu-id="40635-1178">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40635-1179">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1179">No</span></span> |
| <span data-ttu-id="40635-1180">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1180">password</span></span> |<span data-ttu-id="40635-1181">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-1182">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1182">No</span></span> |
| <span data-ttu-id="40635-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1183">gatewayName</span></span> |<span data-ttu-id="40635-1184">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных DB2.</span><span class="sxs-lookup"><span data-stu-id="40635-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="40635-1185">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1186">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1186">Example</span></span>
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
<span data-ttu-id="40635-1187">Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1188">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1188">Dataset</span></span>
<span data-ttu-id="40635-1189">Для определения набора данных DB2 задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="40635-1190">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1190">Property</span></span> | <span data-ttu-id="40635-1191">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1191">Description</span></span> | <span data-ttu-id="40635-1192">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1193">tableName</span></span> |<span data-ttu-id="40635-1194">Имя таблицы в экземпляре базы данных DB2, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="40635-1195">Свойство tableName чувствительно к регистру.</span><span class="sxs-lookup"><span data-stu-id="40635-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="40635-1196">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="40635-1197">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1197">Example</span></span>
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

<span data-ttu-id="40635-1198">Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1199">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1200">При копировании данных из IBM DB2 задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1201">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1201">Property</span></span> | <span data-ttu-id="40635-1202">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1202">Description</span></span> | <span data-ttu-id="40635-1203">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1203">Allowed values</span></span> | <span data-ttu-id="40635-1204">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1205">query</span><span class="sxs-lookup"><span data-stu-id="40635-1205">query</span></span> |<span data-ttu-id="40635-1206">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1207">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1207">SQL query string.</span></span> <span data-ttu-id="40635-1208">Например, `"query": "select * from "MySchema"."MyTable""`.</span><span class="sxs-lookup"><span data-stu-id="40635-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="40635-1209">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1210">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1210">Example</span></span>
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
<span data-ttu-id="40635-1211">Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="40635-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="40635-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1213">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1213">Linked service</span></span>
<span data-ttu-id="40635-1214">Для определения связанной службы MySQL задайте **OnPremisesMySql** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1215">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1215">Property</span></span> | <span data-ttu-id="40635-1216">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1216">Description</span></span> | <span data-ttu-id="40635-1217">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1218">server</span><span class="sxs-lookup"><span data-stu-id="40635-1218">server</span></span> |<span data-ttu-id="40635-1219">Имя сервера MySQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="40635-1220">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1220">Yes</span></span> |
| <span data-ttu-id="40635-1221">database</span><span class="sxs-lookup"><span data-stu-id="40635-1221">database</span></span> |<span data-ttu-id="40635-1222">Имя базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="40635-1223">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1223">Yes</span></span> |
| <span data-ttu-id="40635-1224">schema</span><span class="sxs-lookup"><span data-stu-id="40635-1224">schema</span></span> |<span data-ttu-id="40635-1225">Имя схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="40635-1226">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1226">No</span></span> |
| <span data-ttu-id="40635-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1227">authenticationType</span></span> |<span data-ttu-id="40635-1228">Тип проверки подлинности, используемый для подключения к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="40635-1229">Возможные значения: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="40635-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="40635-1230">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1230">Yes</span></span> |
| <span data-ttu-id="40635-1231">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1231">username</span></span> |<span data-ttu-id="40635-1232">Укажите имя пользователя для подключения к базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="40635-1233">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1233">Yes</span></span> |
| <span data-ttu-id="40635-1234">password</span><span class="sxs-lookup"><span data-stu-id="40635-1234">password</span></span> |<span data-ttu-id="40635-1235">Введите пароль для указанной вами учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="40635-1236">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1236">Yes</span></span> |
| <span data-ttu-id="40635-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1237">gatewayName</span></span> |<span data-ttu-id="40635-1238">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="40635-1239">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1240">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1240">Example</span></span>

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

<span data-ttu-id="40635-1241">Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1242">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1242">Dataset</span></span>
<span data-ttu-id="40635-1243">Для определения набора данных MySQL задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1244">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1244">Property</span></span> | <span data-ttu-id="40635-1245">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1245">Description</span></span> | <span data-ttu-id="40635-1246">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1247">tableName</span></span> |<span data-ttu-id="40635-1248">Имя таблицы в экземпляре базы данных MySQL, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="40635-1249">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1250">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1250">Example</span></span>

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
<span data-ttu-id="40635-1251">Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1252">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1253">При копировании данных из базы данных MySQL задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1254">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1254">Property</span></span> | <span data-ttu-id="40635-1255">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1255">Description</span></span> | <span data-ttu-id="40635-1256">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1256">Allowed values</span></span> | <span data-ttu-id="40635-1257">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1258">query</span><span class="sxs-lookup"><span data-stu-id="40635-1258">query</span></span> |<span data-ttu-id="40635-1259">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1260">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1260">SQL query string.</span></span> <span data-ttu-id="40635-1261">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-1262">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="40635-1263">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1263">Example</span></span>
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

<span data-ttu-id="40635-1264">Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="40635-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="40635-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-1266">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1266">Linked service</span></span>
<span data-ttu-id="40635-1267">Для определения связанной службы Oracle задайте **OnPremisesOracle** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1268">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1268">Property</span></span> | <span data-ttu-id="40635-1269">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1269">Description</span></span> | <span data-ttu-id="40635-1270">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="40635-1271">driverType</span></span> | <span data-ttu-id="40635-1272">Укажите, какой драйвер следует использовать для копирования данных в базу данных Oracle и из нее.</span><span class="sxs-lookup"><span data-stu-id="40635-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="40635-1273">Допустимые значения: **Майкрософт** или **ODP** (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="40635-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="40635-1274">Дополнительные сведения о драйверах см. в разделе [Поддерживаемые версии и установка](#supported-versions-and-installation).</span><span class="sxs-lookup"><span data-stu-id="40635-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="40635-1275">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1275">No</span></span> |
| <span data-ttu-id="40635-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-1276">connectionString</span></span> | <span data-ttu-id="40635-1277">В свойстве connectionString указываются сведения, необходимые для подключения к экземпляру базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="40635-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="40635-1278">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1278">Yes</span></span> |
| <span data-ttu-id="40635-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1279">gatewayName</span></span> | <span data-ttu-id="40635-1280">Имя шлюза, который будет использоваться для подключения к локальному серверу Oracle.</span><span class="sxs-lookup"><span data-stu-id="40635-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="40635-1281">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1282">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1282">Example</span></span>
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

<span data-ttu-id="40635-1283">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1284">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1284">Dataset</span></span>
<span data-ttu-id="40635-1285">Для определения набора данных Oracle задайте **OracleTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1286">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1286">Property</span></span> | <span data-ttu-id="40635-1287">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1287">Description</span></span> | <span data-ttu-id="40635-1288">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1289">tableName</span></span> |<span data-ttu-id="40635-1290">Имя таблицы в базе данных Oracle, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="40635-1291">Нет (если указан параметр **oracleReaderQuery** объекта **OracleSource**)</span><span class="sxs-lookup"><span data-stu-id="40635-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1292">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1292">Example</span></span>

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
<span data-ttu-id="40635-1293">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="40635-1294">Источник Oracle в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="40635-1295">При копировании данных из базы данных Oracle задайте **OracleSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1296">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1296">Property</span></span> | <span data-ttu-id="40635-1297">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1297">Description</span></span> | <span data-ttu-id="40635-1298">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1298">Allowed values</span></span> | <span data-ttu-id="40635-1299">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40635-1300">oracleReaderQuery</span></span> |<span data-ttu-id="40635-1301">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1302">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1302">SQL query string.</span></span> <span data-ttu-id="40635-1303">Например: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="40635-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="40635-1304">Если не указано, то выполняется инструкция SQL `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="40635-1305">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1306">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1306">Example</span></span>

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

<span data-ttu-id="40635-1307">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="40635-1308">Приемник Oracle в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="40635-1309">При копировании данных в базу данных Oracle задайте **OracleSink** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-1310">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1310">Property</span></span> | <span data-ttu-id="40635-1311">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1311">Description</span></span> | <span data-ttu-id="40635-1312">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1312">Allowed values</span></span> | <span data-ttu-id="40635-1313">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-1314">writeBatchTimeout</span></span> |<span data-ttu-id="40635-1315">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="40635-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40635-1316">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="40635-1316">timespan</span></span><br/><br/> <span data-ttu-id="40635-1317">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="40635-1318">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1318">No</span></span> |
| <span data-ttu-id="40635-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-1319">writeBatchSize</span></span> |<span data-ttu-id="40635-1320">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="40635-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="40635-1321">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="40635-1321">Integer (number of rows)</span></span> |<span data-ttu-id="40635-1322">Нет (значение по умолчанию — 100)</span><span class="sxs-lookup"><span data-stu-id="40635-1322">No (default: 100)</span></span> |
| <span data-ttu-id="40635-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40635-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40635-1324">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="40635-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="40635-1325">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-1325">A query statement.</span></span> |<span data-ttu-id="40635-1326">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1326">No</span></span> |
| <span data-ttu-id="40635-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="40635-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="40635-1328">Укажите имя столбца, в которое действие копирования добавляет автоматически созданный идентификатор среза. Этот идентификатор используется для очистки данных конкретного среза при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="40635-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="40635-1329">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="40635-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="40635-1330">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1331">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1331">Example</span></span>
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
<span data-ttu-id="40635-1332">Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="40635-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="40635-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1334">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1334">Linked service</span></span>
<span data-ttu-id="40635-1335">Для определения связанной службы PostgreSQL задайте **OnPremisesPostgreSql** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1336">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1336">Property</span></span> | <span data-ttu-id="40635-1337">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1337">Description</span></span> | <span data-ttu-id="40635-1338">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1339">server</span><span class="sxs-lookup"><span data-stu-id="40635-1339">server</span></span> |<span data-ttu-id="40635-1340">Имя сервера, PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="40635-1341">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1341">Yes</span></span> |
| <span data-ttu-id="40635-1342">database</span><span class="sxs-lookup"><span data-stu-id="40635-1342">database</span></span> |<span data-ttu-id="40635-1343">Имя базы данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="40635-1344">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1344">Yes</span></span> |
| <span data-ttu-id="40635-1345">schema</span><span class="sxs-lookup"><span data-stu-id="40635-1345">schema</span></span> |<span data-ttu-id="40635-1346">Имя схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1346">Name of the schema in the database.</span></span> <span data-ttu-id="40635-1347">Имя схемы чувствительно к регистру.</span><span class="sxs-lookup"><span data-stu-id="40635-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="40635-1348">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1348">No</span></span> |
| <span data-ttu-id="40635-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1349">authenticationType</span></span> |<span data-ttu-id="40635-1350">Тип проверки подлинности, используемый для подключения к базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="40635-1351">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40635-1352">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1352">Yes</span></span> |
| <span data-ttu-id="40635-1353">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1353">username</span></span> |<span data-ttu-id="40635-1354">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40635-1355">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1355">No</span></span> |
| <span data-ttu-id="40635-1356">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1356">password</span></span> |<span data-ttu-id="40635-1357">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-1358">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1358">No</span></span> |
| <span data-ttu-id="40635-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1359">gatewayName</span></span> |<span data-ttu-id="40635-1360">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="40635-1361">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1362">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1362">Example</span></span>

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
<span data-ttu-id="40635-1363">Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1364">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1364">Dataset</span></span>
<span data-ttu-id="40635-1365">Для определения набора данных PostgreSQL задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1366">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1366">Property</span></span> | <span data-ttu-id="40635-1367">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1367">Description</span></span> | <span data-ttu-id="40635-1368">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1369">tableName</span></span> |<span data-ttu-id="40635-1370">Имя таблицы в экземпляре базы данных PostgreSQL, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="40635-1371">Свойство tableName чувствительно к регистру.</span><span class="sxs-lookup"><span data-stu-id="40635-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="40635-1372">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1373">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1373">Example</span></span>
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
<span data-ttu-id="40635-1374">Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1375">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1376">При копировании данных из базы данных PostgreSQL задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1377">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1377">Property</span></span> | <span data-ttu-id="40635-1378">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1378">Description</span></span> | <span data-ttu-id="40635-1379">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1379">Allowed values</span></span> | <span data-ttu-id="40635-1380">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1381">query</span><span class="sxs-lookup"><span data-stu-id="40635-1381">query</span></span> |<span data-ttu-id="40635-1382">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1383">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1383">SQL query string.</span></span> <span data-ttu-id="40635-1384">Например, "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="40635-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="40635-1385">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1386">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1386">Example</span></span>

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

<span data-ttu-id="40635-1387">Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="40635-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="40635-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-1389">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1389">Linked service</span></span>
<span data-ttu-id="40635-1390">Для определения связанной службы SAP Business Warehouse (BW) задайте **SapBw** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="40635-1391">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1391">Property</span></span> | <span data-ttu-id="40635-1392">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1392">Description</span></span> | <span data-ttu-id="40635-1393">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1393">Allowed values</span></span> | <span data-ttu-id="40635-1394">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="40635-1395">server</span><span class="sxs-lookup"><span data-stu-id="40635-1395">server</span></span> | <span data-ttu-id="40635-1396">Имя сервера, на котором размещен экземпляр SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="40635-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="40635-1397">string</span><span class="sxs-lookup"><span data-stu-id="40635-1397">string</span></span> | <span data-ttu-id="40635-1398">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1398">Yes</span></span>
<span data-ttu-id="40635-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="40635-1399">systemNumber</span></span> | <span data-ttu-id="40635-1400">Номер системы SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="40635-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="40635-1401">Двузначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="40635-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="40635-1402">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1402">Yes</span></span>
<span data-ttu-id="40635-1403">clientid</span><span class="sxs-lookup"><span data-stu-id="40635-1403">clientId</span></span> | <span data-ttu-id="40635-1404">Идентификатор клиента в системе SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="40635-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="40635-1405">Трехзначное десятичное число, представленное в виде строки.</span><span class="sxs-lookup"><span data-stu-id="40635-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="40635-1406">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1406">Yes</span></span>
<span data-ttu-id="40635-1407">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1407">username</span></span> | <span data-ttu-id="40635-1408">Имя пользователя, имеющего доступ к серверу SAP.</span><span class="sxs-lookup"><span data-stu-id="40635-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="40635-1409">строка</span><span class="sxs-lookup"><span data-stu-id="40635-1409">string</span></span> | <span data-ttu-id="40635-1410">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1410">Yes</span></span>
<span data-ttu-id="40635-1411">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1411">password</span></span> | <span data-ttu-id="40635-1412">Пароль для пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1412">Password for the user.</span></span> | <span data-ttu-id="40635-1413">string</span><span class="sxs-lookup"><span data-stu-id="40635-1413">string</span></span> | <span data-ttu-id="40635-1414">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1414">Yes</span></span>
<span data-ttu-id="40635-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1415">gatewayName</span></span> | <span data-ttu-id="40635-1416">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальному экземпляру SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="40635-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="40635-1417">строка</span><span class="sxs-lookup"><span data-stu-id="40635-1417">string</span></span> | <span data-ttu-id="40635-1418">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1418">Yes</span></span>
<span data-ttu-id="40635-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-1419">encryptedCredential</span></span> | <span data-ttu-id="40635-1420">Строка зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1420">The encrypted credential string.</span></span> | <span data-ttu-id="40635-1421">string</span><span class="sxs-lookup"><span data-stu-id="40635-1421">string</span></span> | <span data-ttu-id="40635-1422">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="40635-1423">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1423">Example</span></span>

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

<span data-ttu-id="40635-1424">Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1425">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1425">Dataset</span></span>
<span data-ttu-id="40635-1426">Для определения набора данных SAP BW задайте **RelationalTable** в качестве **типа** набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="40635-1427">Для набора данных SAP Business Warehouse типа **RelationalTable** не поддерживаются какие-либо свойства типа.</span><span class="sxs-lookup"><span data-stu-id="40635-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="40635-1428">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1428">Example</span></span>

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
<span data-ttu-id="40635-1429">Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1430">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1431">При копировании данных из SAP Business Warehouse задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1432">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1432">Property</span></span> | <span data-ttu-id="40635-1433">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1433">Description</span></span> | <span data-ttu-id="40635-1434">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1434">Allowed values</span></span> | <span data-ttu-id="40635-1435">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1436">query</span><span class="sxs-lookup"><span data-stu-id="40635-1436">query</span></span> | <span data-ttu-id="40635-1437">Указывает запрос многомерных выражений для чтения данных из экземпляра SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="40635-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="40635-1438">Запрос многомерных выражений.</span><span class="sxs-lookup"><span data-stu-id="40635-1438">MDX query.</span></span> | <span data-ttu-id="40635-1439">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1440">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1440">Example</span></span>

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

<span data-ttu-id="40635-1441">Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="40635-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="40635-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1443">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1443">Linked service</span></span>
<span data-ttu-id="40635-1444">Для определения связанной службы SAP HANA задайте **SapHana** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="40635-1445">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1445">Property</span></span> | <span data-ttu-id="40635-1446">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1446">Description</span></span> | <span data-ttu-id="40635-1447">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1447">Allowed values</span></span> | <span data-ttu-id="40635-1448">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="40635-1449">server</span><span class="sxs-lookup"><span data-stu-id="40635-1449">server</span></span> | <span data-ttu-id="40635-1450">Имя сервера, на котором размещен экземпляр SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="40635-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="40635-1451">Если ваш сервер использует настроенный порт, укажите `server:port`.</span><span class="sxs-lookup"><span data-stu-id="40635-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="40635-1452">строка</span><span class="sxs-lookup"><span data-stu-id="40635-1452">string</span></span> | <span data-ttu-id="40635-1453">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1453">Yes</span></span>
<span data-ttu-id="40635-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1454">authenticationType</span></span> | <span data-ttu-id="40635-1455">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="40635-1455">Type of authentication.</span></span> | <span data-ttu-id="40635-1456">string.</span><span class="sxs-lookup"><span data-stu-id="40635-1456">string.</span></span> <span data-ttu-id="40635-1457">Basic или Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="40635-1458">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1458">Yes</span></span> 
<span data-ttu-id="40635-1459">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1459">username</span></span> | <span data-ttu-id="40635-1460">Имя пользователя, имеющего доступ к серверу SAP.</span><span class="sxs-lookup"><span data-stu-id="40635-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="40635-1461">строка</span><span class="sxs-lookup"><span data-stu-id="40635-1461">string</span></span> | <span data-ttu-id="40635-1462">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1462">Yes</span></span>
<span data-ttu-id="40635-1463">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1463">password</span></span> | <span data-ttu-id="40635-1464">Пароль для пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1464">Password for the user.</span></span> | <span data-ttu-id="40635-1465">string</span><span class="sxs-lookup"><span data-stu-id="40635-1465">string</span></span> | <span data-ttu-id="40635-1466">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1466">Yes</span></span>
<span data-ttu-id="40635-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1467">gatewayName</span></span> | <span data-ttu-id="40635-1468">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальному экземпляру SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="40635-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="40635-1469">строка</span><span class="sxs-lookup"><span data-stu-id="40635-1469">string</span></span> | <span data-ttu-id="40635-1470">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1470">Yes</span></span>
<span data-ttu-id="40635-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-1471">encryptedCredential</span></span> | <span data-ttu-id="40635-1472">Строка зашифрованных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1472">The encrypted credential string.</span></span> | <span data-ttu-id="40635-1473">string</span><span class="sxs-lookup"><span data-stu-id="40635-1473">string</span></span> | <span data-ttu-id="40635-1474">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="40635-1475">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1475">Example</span></span>

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
<span data-ttu-id="40635-1476">Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="40635-1477">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1477">Dataset</span></span>
<span data-ttu-id="40635-1478">Для определения набора данных SAP HANA задайте **RelationalTable** в качестве **типа** набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="40635-1479">Для набора данных SAP HANA типа **RelationalTable** не поддерживаются какие-либо свойства типа.</span><span class="sxs-lookup"><span data-stu-id="40635-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="40635-1480">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1480">Example</span></span>

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
<span data-ttu-id="40635-1481">Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1482">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1483">При копировании данных из хранилища данных SAP HANA задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1484">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1484">Property</span></span> | <span data-ttu-id="40635-1485">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1485">Description</span></span> | <span data-ttu-id="40635-1486">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1486">Allowed values</span></span> | <span data-ttu-id="40635-1487">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1488">query</span><span class="sxs-lookup"><span data-stu-id="40635-1488">query</span></span> | <span data-ttu-id="40635-1489">Указывает SQL-запрос для чтения данных из экземпляра SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="40635-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="40635-1490">SQL-запрос.</span><span class="sxs-lookup"><span data-stu-id="40635-1490">SQL query.</span></span> | <span data-ttu-id="40635-1491">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="40635-1492">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1492">Example</span></span>


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

<span data-ttu-id="40635-1493">Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="40635-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40635-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1495">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1495">Linked service</span></span>
<span data-ttu-id="40635-1496">Создайте связанную службу типа **OnPremisesSqlServer**, чтобы связать локальную базу данных SQL Server с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="40635-1497">В следующей таблице содержится описание элементов JSON, которые относятся к локальной связанной службе SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="40635-1498">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="40635-1499">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1499">Property</span></span> | <span data-ttu-id="40635-1500">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1500">Description</span></span> | <span data-ttu-id="40635-1501">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1502">type</span><span class="sxs-lookup"><span data-stu-id="40635-1502">type</span></span> |<span data-ttu-id="40635-1503">Свойству type необходимо присвоить значение **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="40635-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="40635-1504">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1504">Yes</span></span> |
| <span data-ttu-id="40635-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-1505">connectionString</span></span> |<span data-ttu-id="40635-1506">Укажите сведения о параметре connectionString, необходимые для подключения к локальной базе данных SQL Server с помощью проверки подлинности SQL или проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="40635-1507">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1507">Yes</span></span> |
| <span data-ttu-id="40635-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1508">gatewayName</span></span> |<span data-ttu-id="40635-1509">Имя шлюза, который службе фабрики данных следует использовать для подключения к локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="40635-1510">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1510">Yes</span></span> |
| <span data-ttu-id="40635-1511">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1511">username</span></span> |<span data-ttu-id="40635-1512">При использовании проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="40635-1513">Например, **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="40635-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="40635-1514">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1514">No</span></span> |
| <span data-ttu-id="40635-1515">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1515">password</span></span> |<span data-ttu-id="40635-1516">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-1517">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1517">No</span></span> |

<span data-ttu-id="40635-1518">Вы можете зашифровать учетные данные с помощью командлета **New-AzureRmDataFactoryEncryptValue** и использовать их в строке подключения, как показано в следующем примере (свойство **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="40635-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="40635-1519">Пример: JSON для использования проверки подлинности SQL</span><span class="sxs-lookup"><span data-stu-id="40635-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="40635-1520">Пример: JSON для использования проверки подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="40635-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="40635-1521">Если указаны имя пользователя и пароль, то шлюз использует их, чтобы действовать от имени соответствующей учетной записи пользователя для подключения к локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="40635-1522">В противном случае шлюз подключается к SQL Server напрямую с помощью контекста безопасности шлюза (его стартовая учетная запись).</span><span class="sxs-lookup"><span data-stu-id="40635-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="40635-1523">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1524">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1524">Dataset</span></span>
<span data-ttu-id="40635-1525">Для определения набора данных SQL Server задайте **SqlServerTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1526">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1526">Property</span></span> | <span data-ttu-id="40635-1527">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1527">Description</span></span> | <span data-ttu-id="40635-1528">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1529">tableName</span></span> |<span data-ttu-id="40635-1530">Имя таблицы или представления в экземпляре базы данных SQL Server, на который ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="40635-1531">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1532">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1532">Example</span></span>
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

<span data-ttu-id="40635-1533">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="40635-1534">Источник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="40635-1535">При копировании данных из базы данных SQL Server задайте **SqlSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1536">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1536">Property</span></span> | <span data-ttu-id="40635-1537">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1537">Description</span></span> | <span data-ttu-id="40635-1538">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1538">Allowed values</span></span> | <span data-ttu-id="40635-1539">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="40635-1540">sqlReaderQuery</span></span> |<span data-ttu-id="40635-1541">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1542">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1542">SQL query string.</span></span> <span data-ttu-id="40635-1543">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="40635-1544">Может ссылаться на несколько таблиц из базы данных, на которую ссылается входной набор данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="40635-1545">Если не указано другое, выполняется инструкция SQL select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="40635-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="40635-1546">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1546">No</span></span> |
| <span data-ttu-id="40635-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40635-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="40635-1548">Имя хранимой процедуры, которая считывает данные из исходной таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="40635-1549">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="40635-1550">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1550">No</span></span> |
| <span data-ttu-id="40635-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40635-1551">storedProcedureParameters</span></span> |<span data-ttu-id="40635-1552">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40635-1553">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="40635-1553">Name/value pairs.</span></span> <span data-ttu-id="40635-1554">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40635-1555">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1555">No</span></span> |

<span data-ttu-id="40635-1556">Если для SqlSource указано **sqlReaderQuery** , то действие копирования выполняет этот запрос для источника базы данных SQL Server с целью получения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="40635-1557">Кроме того, можно создать хранимую процедуру, указав **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="40635-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="40635-1558">Если не указать sqlReaderQuery или sqlReaderStoredProcedureName, то для построения запроса select к базе данных SQL Server будут использованы столбцы, определенные в разделе структуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="40635-1559">Если у определения набора данных нет структуры, выбираются все столбцы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="40635-1560">При использовании **sqlReaderStoredProcedureName** по-прежнему необходимо указать значение свойства **tableName** в наборе данных JSON.</span><span class="sxs-lookup"><span data-stu-id="40635-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="40635-1561">Хотя какие-либо проверки этой таблицы отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="40635-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="40635-1562">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1562">Example</span></span>
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

<span data-ttu-id="40635-1563">В этом примере для свойства SqlSource указано **sqlReaderQuery** .</span><span class="sxs-lookup"><span data-stu-id="40635-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="40635-1564">Действие копирования выполняет этот запрос к источнику базы данных SQL Server с целью получения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="40635-1565">Кроме того, можно создать хранимую процедуру, указав **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если хранимая процедура принимает параметры).</span><span class="sxs-lookup"><span data-stu-id="40635-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="40635-1566">Свойство sqlReaderQuery может ссылаться на несколько таблиц из базы данных, на которую ссылается входной набор данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="40635-1567">Он не ограничивается таблицей, заданной свойством typeProperty в качестве параметра tableName набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="40635-1568">Если не указать sqlReaderQuery или sqlReaderStoredProcedureName, то для построения запроса select к базе данных SQL Server будут использованы столбцы, определенные в разделе структуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="40635-1569">Если у определения набора данных нет структуры, выбираются все столбцы из таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="40635-1570">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="40635-1571">Приемник SQL в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="40635-1572">При копировании данных в базу данных SQL Server задайте **SqlSink** в качестве **типа приемника** для действия копирования и укажите в разделе **sink** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-1573">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1573">Property</span></span> | <span data-ttu-id="40635-1574">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1574">Description</span></span> | <span data-ttu-id="40635-1575">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1575">Allowed values</span></span> | <span data-ttu-id="40635-1576">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-1577">writeBatchTimeout</span></span> |<span data-ttu-id="40635-1578">Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.</span><span class="sxs-lookup"><span data-stu-id="40635-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="40635-1579">Интервал времени</span><span class="sxs-lookup"><span data-stu-id="40635-1579">timespan</span></span><br/><br/> <span data-ttu-id="40635-1580">Пример: 00:30:00 (30 минут).</span><span class="sxs-lookup"><span data-stu-id="40635-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="40635-1581">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1581">No</span></span> |
| <span data-ttu-id="40635-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="40635-1582">writeBatchSize</span></span> |<span data-ttu-id="40635-1583">Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="40635-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="40635-1584">Целое число (количество строк)</span><span class="sxs-lookup"><span data-stu-id="40635-1584">Integer (number of rows)</span></span> |<span data-ttu-id="40635-1585">Нет (значение по умолчанию — 10 000).</span><span class="sxs-lookup"><span data-stu-id="40635-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="40635-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="40635-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="40635-1587">Укажите запрос на выполнение действия копирования, позволяющий убедиться в том, что данные конкретного среза очищены.</span><span class="sxs-lookup"><span data-stu-id="40635-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="40635-1588">Дополнительные сведения см. в разделе о [повторяемости](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="40635-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="40635-1589">Инструкция запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-1589">A query statement.</span></span> |<span data-ttu-id="40635-1590">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1590">No</span></span> |
| <span data-ttu-id="40635-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="40635-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="40635-1592">Укажите имя столбца, в которое действие копирования добавляет автоматически созданный идентификатор среза. Этот идентификатор используется для очистки данных конкретного среза при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="40635-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="40635-1593">Дополнительные сведения см. в разделе о [повторяемости](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="40635-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="40635-1594">Имя столбца с типом данных binary(32).</span><span class="sxs-lookup"><span data-stu-id="40635-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="40635-1595">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1595">No</span></span> |
| <span data-ttu-id="40635-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="40635-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="40635-1597">Имя хранимой процедуры, обновляющей данные или вставляющей их в целевую таблицу.</span><span class="sxs-lookup"><span data-stu-id="40635-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="40635-1598">Имя хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="40635-1599">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1599">No</span></span> |
| <span data-ttu-id="40635-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40635-1600">storedProcedureParameters</span></span> |<span data-ttu-id="40635-1601">Параметры для хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="40635-1602">Пары имен и значений.</span><span class="sxs-lookup"><span data-stu-id="40635-1602">Name/value pairs.</span></span> <span data-ttu-id="40635-1603">Имена и регистр параметров должны совпадать с именами и регистром параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="40635-1604">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1604">No</span></span> |
| <span data-ttu-id="40635-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="40635-1605">sqlWriterTableType</span></span> |<span data-ttu-id="40635-1606">Укажите имя типа таблицы для использования в хранимой процедуре.</span><span class="sxs-lookup"><span data-stu-id="40635-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="40635-1607">Действие копирования делает перемещаемые данные доступными во временной таблице этого типа.</span><span class="sxs-lookup"><span data-stu-id="40635-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="40635-1608">Код хранимой процедуры затем можно использовать для объединения копируемых и существующих данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="40635-1609">Имя типа таблицы.</span><span class="sxs-lookup"><span data-stu-id="40635-1609">A table type name.</span></span> |<span data-ttu-id="40635-1610">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1611">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1611">Example</span></span>
<span data-ttu-id="40635-1612">Конвейер содержит действие копирования, которое использует эти входной и выходной наборы данных и выполняется каждый час.</span><span class="sxs-lookup"><span data-stu-id="40635-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="40635-1613">В определении JSON конвейера для типа **source** установлено значение **BlobSource**, а для типа **sink** — значение **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="40635-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

<span data-ttu-id="40635-1614">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="40635-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="40635-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1616">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1616">Linked service</span></span>
<span data-ttu-id="40635-1617">Для определения связанной службы Sybase задайте **OnPremisesSybase** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1618">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1618">Property</span></span> | <span data-ttu-id="40635-1619">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1619">Description</span></span> | <span data-ttu-id="40635-1620">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1621">server</span><span class="sxs-lookup"><span data-stu-id="40635-1621">server</span></span> |<span data-ttu-id="40635-1622">Имя сервера Sybase.</span><span class="sxs-lookup"><span data-stu-id="40635-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="40635-1623">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1623">Yes</span></span> |
| <span data-ttu-id="40635-1624">database</span><span class="sxs-lookup"><span data-stu-id="40635-1624">database</span></span> |<span data-ttu-id="40635-1625">Имя базы данных Sybase.</span><span class="sxs-lookup"><span data-stu-id="40635-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="40635-1626">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1626">Yes</span></span> |
| <span data-ttu-id="40635-1627">schema</span><span class="sxs-lookup"><span data-stu-id="40635-1627">schema</span></span> |<span data-ttu-id="40635-1628">Имя схемы в базе данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="40635-1629">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1629">No</span></span> |
| <span data-ttu-id="40635-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1630">authenticationType</span></span> |<span data-ttu-id="40635-1631">Тип проверки подлинности, используемый для подключения к базе данных Sybase.</span><span class="sxs-lookup"><span data-stu-id="40635-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="40635-1632">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40635-1633">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1633">Yes</span></span> |
| <span data-ttu-id="40635-1634">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1634">username</span></span> |<span data-ttu-id="40635-1635">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40635-1636">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1636">No</span></span> |
| <span data-ttu-id="40635-1637">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1637">password</span></span> |<span data-ttu-id="40635-1638">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-1639">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1639">No</span></span> |
| <span data-ttu-id="40635-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1640">gatewayName</span></span> |<span data-ttu-id="40635-1641">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных Sybase.</span><span class="sxs-lookup"><span data-stu-id="40635-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="40635-1642">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1643">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1643">Example</span></span>
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

<span data-ttu-id="40635-1644">Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1645">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1645">Dataset</span></span>
<span data-ttu-id="40635-1646">Для определения набора данных Sybase задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1647">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1647">Property</span></span> | <span data-ttu-id="40635-1648">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1648">Description</span></span> | <span data-ttu-id="40635-1649">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1650">tableName</span></span> |<span data-ttu-id="40635-1651">Имя таблицы в экземпляре базы данных Sybase, на которое ссылается связанная служба.</span><span class="sxs-lookup"><span data-stu-id="40635-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="40635-1652">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1653">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1653">Example</span></span>

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

<span data-ttu-id="40635-1654">Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1655">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1656">При копировании данных из базы данных Sybase задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1657">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1657">Property</span></span> | <span data-ttu-id="40635-1658">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1658">Description</span></span> | <span data-ttu-id="40635-1659">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1659">Allowed values</span></span> | <span data-ttu-id="40635-1660">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1661">query</span><span class="sxs-lookup"><span data-stu-id="40635-1661">query</span></span> |<span data-ttu-id="40635-1662">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1663">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1663">SQL query string.</span></span> <span data-ttu-id="40635-1664">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-1665">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1666">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1666">Example</span></span>

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

<span data-ttu-id="40635-1667">Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="40635-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="40635-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1669">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1669">Linked service</span></span>
<span data-ttu-id="40635-1670">Для определения связанной службы Teradata задайте **OnPremisesTeradata** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1671">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1671">Property</span></span> | <span data-ttu-id="40635-1672">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1672">Description</span></span> | <span data-ttu-id="40635-1673">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1674">server</span><span class="sxs-lookup"><span data-stu-id="40635-1674">server</span></span> |<span data-ttu-id="40635-1675">Имя сервера Teradata.</span><span class="sxs-lookup"><span data-stu-id="40635-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="40635-1676">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1676">Yes</span></span> |
| <span data-ttu-id="40635-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1677">authenticationType</span></span> |<span data-ttu-id="40635-1678">Тип проверки подлинности, используемый для подключения к базе данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="40635-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="40635-1679">Возможными значениями являются: анонимная, обычная и Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40635-1680">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1680">Yes</span></span> |
| <span data-ttu-id="40635-1681">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1681">username</span></span> |<span data-ttu-id="40635-1682">При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="40635-1683">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1683">No</span></span> |
| <span data-ttu-id="40635-1684">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1684">password</span></span> |<span data-ttu-id="40635-1685">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-1686">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1686">No</span></span> |
| <span data-ttu-id="40635-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1687">gatewayName</span></span> |<span data-ttu-id="40635-1688">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="40635-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="40635-1689">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1690">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1690">Example</span></span>
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

<span data-ttu-id="40635-1691">Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1692">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1692">Dataset</span></span>
<span data-ttu-id="40635-1693">Для определения набора данных больших двоичных объектов Teradata задайте **RelationalTable** в качестве **типа** набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="40635-1694">Сейчас нет каких-либо свойств типа, поддерживаемых для набора данных Teradata.</span><span class="sxs-lookup"><span data-stu-id="40635-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="40635-1695">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1695">Example</span></span>
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

<span data-ttu-id="40635-1696">Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-1697">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-1698">При копировании данных из базы данных Teradata задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1699">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1699">Property</span></span> | <span data-ttu-id="40635-1700">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1700">Description</span></span> | <span data-ttu-id="40635-1701">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1701">Allowed values</span></span> | <span data-ttu-id="40635-1702">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1703">query</span><span class="sxs-lookup"><span data-stu-id="40635-1703">query</span></span> |<span data-ttu-id="40635-1704">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1705">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1705">SQL query string.</span></span> <span data-ttu-id="40635-1706">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-1707">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1708">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1708">Example</span></span>

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

<span data-ttu-id="40635-1709">Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="40635-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="40635-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-1711">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1711">Linked service</span></span>
<span data-ttu-id="40635-1712">Для определения связанной службы Cassandra задайте **OnPremisesCassandra** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1713">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1713">Property</span></span> | <span data-ttu-id="40635-1714">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1714">Description</span></span> | <span data-ttu-id="40635-1715">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1716">host</span><span class="sxs-lookup"><span data-stu-id="40635-1716">host</span></span> |<span data-ttu-id="40635-1717">Один или несколько IP-адресов или имен узлов серверов Cassandra.</span><span class="sxs-lookup"><span data-stu-id="40635-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="40635-1718">Укажите через запятую список IP-адресов или имен узлов для одновременного подключения ко всем серверам.</span><span class="sxs-lookup"><span data-stu-id="40635-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="40635-1719">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1719">Yes</span></span> |
| <span data-ttu-id="40635-1720">порт</span><span class="sxs-lookup"><span data-stu-id="40635-1720">port</span></span> |<span data-ttu-id="40635-1721">TCP-порт, используемый сервером Cassandra для прослушивания клиентских подключений</span><span class="sxs-lookup"><span data-stu-id="40635-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="40635-1722">Нет. Значение по умолчанию — 9042</span><span class="sxs-lookup"><span data-stu-id="40635-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="40635-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1723">authenticationType</span></span> |<span data-ttu-id="40635-1724">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="40635-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="40635-1725">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1725">Yes</span></span> |
| <span data-ttu-id="40635-1726">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1726">username</span></span> |<span data-ttu-id="40635-1727">Укажите имя пользователя для учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="40635-1728">Да (если для свойства authenticationType задано значение Basic)</span><span class="sxs-lookup"><span data-stu-id="40635-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="40635-1729">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1729">password</span></span> |<span data-ttu-id="40635-1730">Укажите пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-1730">Specify password for the user account.</span></span> |<span data-ttu-id="40635-1731">Да (если для свойства authenticationType задано значение Basic)</span><span class="sxs-lookup"><span data-stu-id="40635-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="40635-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1732">gatewayName</span></span> |<span data-ttu-id="40635-1733">Имя шлюза, который используется для подключения к локальной базе данных Cassandra.</span><span class="sxs-lookup"><span data-stu-id="40635-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="40635-1734">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1734">Yes</span></span> |
| <span data-ttu-id="40635-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-1735">encryptedCredential</span></span> |<span data-ttu-id="40635-1736">Учетные данные, зашифрованные шлюзом</span><span class="sxs-lookup"><span data-stu-id="40635-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="40635-1737">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1738">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1738">Example</span></span>

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

<span data-ttu-id="40635-1739">Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-1740">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1740">Dataset</span></span>
<span data-ttu-id="40635-1741">Для определения набора данных Cassandra задайте **CassandraTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1742">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1742">Property</span></span> | <span data-ttu-id="40635-1743">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1743">Description</span></span> | <span data-ttu-id="40635-1744">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="40635-1745">keyspace</span></span> |<span data-ttu-id="40635-1746">Имя пространства ключей или схемы в базе данных Cassandra</span><span class="sxs-lookup"><span data-stu-id="40635-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="40635-1747">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="40635-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-1748">tableName</span></span> |<span data-ttu-id="40635-1749">Имя таблицы в базе данных Cassandra</span><span class="sxs-lookup"><span data-stu-id="40635-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="40635-1750">Да (если для **CassandraSource** не определено значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1751">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1751">Example</span></span>

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

<span data-ttu-id="40635-1752">Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="40635-1753">Источник Cassandra в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="40635-1754">При копировании данных из Cassandra задайте **CassandraSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1755">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1755">Property</span></span> | <span data-ttu-id="40635-1756">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1756">Description</span></span> | <span data-ttu-id="40635-1757">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1757">Allowed values</span></span> | <span data-ttu-id="40635-1758">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1759">query</span><span class="sxs-lookup"><span data-stu-id="40635-1759">query</span></span> |<span data-ttu-id="40635-1760">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1761">Запрос SQL-92 или CQL.</span><span class="sxs-lookup"><span data-stu-id="40635-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="40635-1762">Ознакомьтесь со [справочником по CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="40635-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="40635-1763">Если используется SQL-запрос, то таблицу, к которой необходимо отправить запрос, укажите в формате **имя_пространства_ключей.имя_таблицы**.</span><span class="sxs-lookup"><span data-stu-id="40635-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="40635-1764">Нет (если в наборе данных определены свойства tableName и keyspace)</span><span class="sxs-lookup"><span data-stu-id="40635-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="40635-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="40635-1765">consistencyLevel</span></span> |<span data-ttu-id="40635-1766">Определяет количество реплик, которые должны ответить на запрос на чтение перед возвращением данных в клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="40635-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="40635-1767">Чтобы выполнить запрос на чтение, база данных Cassandra проверяет наличие указанного количества реплик для данных</span><span class="sxs-lookup"><span data-stu-id="40635-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="40635-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="40635-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="40635-1769">Дополнительные сведения см. в статье [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Настройка согласованности данных).</span><span class="sxs-lookup"><span data-stu-id="40635-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="40635-1770">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-1770">No.</span></span> <span data-ttu-id="40635-1771">Значение по умолчанию — ONE</span><span class="sxs-lookup"><span data-stu-id="40635-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1772">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
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

<span data-ttu-id="40635-1773">Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="40635-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="40635-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-1775">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1775">Linked service</span></span>
<span data-ttu-id="40635-1776">Для определения связанной службы MongoDB задайте **OnPremisesMongoDB** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1777">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1777">Property</span></span> | <span data-ttu-id="40635-1778">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1778">Description</span></span> | <span data-ttu-id="40635-1779">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1780">server</span><span class="sxs-lookup"><span data-stu-id="40635-1780">server</span></span> |<span data-ttu-id="40635-1781">IP-адрес или имя узла сервера MongoDB</span><span class="sxs-lookup"><span data-stu-id="40635-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="40635-1782">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1782">Yes</span></span> |
| <span data-ttu-id="40635-1783">порт</span><span class="sxs-lookup"><span data-stu-id="40635-1783">port</span></span> |<span data-ttu-id="40635-1784">TCP-порт, используемый сервером MongoDB для прослушивания клиентских подключений</span><span class="sxs-lookup"><span data-stu-id="40635-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="40635-1785">Значение по умолчанию — 27017 (необязательно)</span><span class="sxs-lookup"><span data-stu-id="40635-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="40635-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-1786">authenticationType</span></span> |<span data-ttu-id="40635-1787">Укажите тип Basic или Anonymous</span><span class="sxs-lookup"><span data-stu-id="40635-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="40635-1788">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1788">Yes</span></span> |
| <span data-ttu-id="40635-1789">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1789">username</span></span> |<span data-ttu-id="40635-1790">Учетная запись пользователя для доступа к MongoDB</span><span class="sxs-lookup"><span data-stu-id="40635-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="40635-1791">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="40635-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="40635-1792">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1792">password</span></span> |<span data-ttu-id="40635-1793">Пароль для пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-1793">Password for the user.</span></span> |<span data-ttu-id="40635-1794">Да (если используется обычная проверка подлинности)</span><span class="sxs-lookup"><span data-stu-id="40635-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="40635-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="40635-1795">authSource</span></span> |<span data-ttu-id="40635-1796">Имя базы данных MongoDB, которое будет использоваться для проверки учетных данных при проверке подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="40635-1797">Необязательно (если используется обычная проверка подлинности).</span><span class="sxs-lookup"><span data-stu-id="40635-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="40635-1798">По умолчанию используется учетная запись администратора и база данных, указанная с помощью свойства databaseName</span><span class="sxs-lookup"><span data-stu-id="40635-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="40635-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="40635-1799">databaseName</span></span> |<span data-ttu-id="40635-1800">Имя базы данных MongoDB, к которой необходимо получить доступ</span><span class="sxs-lookup"><span data-stu-id="40635-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="40635-1801">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1801">Yes</span></span> |
| <span data-ttu-id="40635-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1802">gatewayName</span></span> |<span data-ttu-id="40635-1803">Имя шлюза, который обращается к хранилищу данных</span><span class="sxs-lookup"><span data-stu-id="40635-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="40635-1804">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1804">Yes</span></span> |
| <span data-ttu-id="40635-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-1805">encryptedCredential</span></span> |<span data-ttu-id="40635-1806">Учетные данные, зашифрованные шлюзом</span><span class="sxs-lookup"><span data-stu-id="40635-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="40635-1807">Необязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1808">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="40635-1809">Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1810">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1810">Dataset</span></span>
<span data-ttu-id="40635-1811">Для определения набора данных MongoDB задайте **Collection** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1812">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1812">Property</span></span> | <span data-ttu-id="40635-1813">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1813">Description</span></span> | <span data-ttu-id="40635-1814">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="40635-1815">collectionName</span></span> |<span data-ttu-id="40635-1816">Имя коллекции в базе данных MongoDB</span><span class="sxs-lookup"><span data-stu-id="40635-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="40635-1817">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1818">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1818">Example</span></span>

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

<span data-ttu-id="40635-1819">Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="40635-1820">Источник MongoDB в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="40635-1821">При копировании данных из MongoDB задайте **MongoDbSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1822">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1822">Property</span></span> | <span data-ttu-id="40635-1823">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1823">Description</span></span> | <span data-ttu-id="40635-1824">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1824">Allowed values</span></span> | <span data-ttu-id="40635-1825">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1826">query</span><span class="sxs-lookup"><span data-stu-id="40635-1826">query</span></span> |<span data-ttu-id="40635-1827">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-1828">Строка запроса SQL-92.</span><span class="sxs-lookup"><span data-stu-id="40635-1828">SQL-92 query string.</span></span> <span data-ttu-id="40635-1829">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-1830">Нет (если для свойства **collectionName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1831">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1831">Example</span></span>

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

<span data-ttu-id="40635-1832">Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="40635-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="40635-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-1834">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1834">Linked service</span></span>
<span data-ttu-id="40635-1835">Для определения связанной службы S3 задайте **AwsAccessKey** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-1836">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1836">Property</span></span> | <span data-ttu-id="40635-1837">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1837">Description</span></span> | <span data-ttu-id="40635-1838">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1838">Allowed values</span></span> | <span data-ttu-id="40635-1839">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="40635-1840">accessKeyID</span></span> |<span data-ttu-id="40635-1841">Идентификатор секретного ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="40635-1841">ID of the secret access key.</span></span> |<span data-ttu-id="40635-1842">string</span><span class="sxs-lookup"><span data-stu-id="40635-1842">string</span></span> |<span data-ttu-id="40635-1843">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1843">Yes</span></span> |
| <span data-ttu-id="40635-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="40635-1844">secretAccessKey</span></span> |<span data-ttu-id="40635-1845">Сам секретный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="40635-1845">The secret access key itself.</span></span> |<span data-ttu-id="40635-1846">Зашифрованная строка секрета</span><span class="sxs-lookup"><span data-stu-id="40635-1846">Encrypted secret string</span></span> |<span data-ttu-id="40635-1847">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-1848">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1848">Example</span></span>
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

<span data-ttu-id="40635-1849">Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1850">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1850">Dataset</span></span>
<span data-ttu-id="40635-1851">Для определения набора данных Amazon S3 задайте **AmazonS3** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1852">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1852">Property</span></span> | <span data-ttu-id="40635-1853">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1853">Description</span></span> | <span data-ttu-id="40635-1854">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1854">Allowed values</span></span> | <span data-ttu-id="40635-1855">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="40635-1856">bucketName</span></span> |<span data-ttu-id="40635-1857">Имя контейнера S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1857">The S3 bucket name.</span></span> |<span data-ttu-id="40635-1858">string</span><span class="sxs-lookup"><span data-stu-id="40635-1858">String</span></span> |<span data-ttu-id="40635-1859">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1859">Yes</span></span> |
| <span data-ttu-id="40635-1860">key</span><span class="sxs-lookup"><span data-stu-id="40635-1860">key</span></span> |<span data-ttu-id="40635-1861">Ключ объекта S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1861">The S3 object key.</span></span> |<span data-ttu-id="40635-1862">string</span><span class="sxs-lookup"><span data-stu-id="40635-1862">String</span></span> |<span data-ttu-id="40635-1863">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1863">No</span></span> |
| <span data-ttu-id="40635-1864">prefix</span><span class="sxs-lookup"><span data-stu-id="40635-1864">prefix</span></span> |<span data-ttu-id="40635-1865">Префикс для ключа объекта S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="40635-1866">Выбираются объекты, ключи которых начинаются с этого префикса.</span><span class="sxs-lookup"><span data-stu-id="40635-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="40635-1867">Применяется, только если ключ пустой.</span><span class="sxs-lookup"><span data-stu-id="40635-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="40635-1868">string</span><span class="sxs-lookup"><span data-stu-id="40635-1868">String</span></span> |<span data-ttu-id="40635-1869">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1869">No</span></span> |
| <span data-ttu-id="40635-1870">версия</span><span class="sxs-lookup"><span data-stu-id="40635-1870">version</span></span> |<span data-ttu-id="40635-1871">Версия объекта S3, если включено управление версиями S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="40635-1872">string</span><span class="sxs-lookup"><span data-stu-id="40635-1872">String</span></span> |<span data-ttu-id="40635-1873">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1873">No</span></span> |
| <span data-ttu-id="40635-1874">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-1874">format</span></span> | <span data-ttu-id="40635-1875">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-1876">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-1877">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-1878">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-1879">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1879">No</span></span> | |
| <span data-ttu-id="40635-1880">compression</span><span class="sxs-lookup"><span data-stu-id="40635-1880">compression</span></span> | <span data-ttu-id="40635-1881">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-1882">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40635-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40635-1883">Поддерживаемые уровни: **Optimal** (Оптимальный) и **Fastest** (Самый быстрый).</span><span class="sxs-lookup"><span data-stu-id="40635-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-1884">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-1885">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="40635-1886">Свойства bucketName и key указывают расположение объекта S3, где контейнер — это корневой контейнер для объектов S3, а ключ — это полный путь к объекту S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="40635-1887">Пример: пример набора данных с префиксом</span><span class="sxs-lookup"><span data-stu-id="40635-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="40635-1888">Пример: пример набора данных (с версией)</span><span class="sxs-lookup"><span data-stu-id="40635-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="40635-1889">Пример: динамические пути для S3</span><span class="sxs-lookup"><span data-stu-id="40635-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="40635-1890">В этом примере мы используем фиксированные значения для свойств key и bucketName в наборе данных Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="40635-1891">Можно настроить фабрику данных для динамического вычисления значений свойств key и bucketName во время выполнения с помощью системных переменных, например SliceStart.</span><span class="sxs-lookup"><span data-stu-id="40635-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="40635-1892">То же самое можно сделать и для свойства prefix набора данных Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="40635-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="40635-1893">В статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md) приведен список поддерживаемых функций и переменных.</span><span class="sxs-lookup"><span data-stu-id="40635-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="40635-1894">Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40635-1895">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="40635-1896">При копировании данных из Amazon S3 задайте **FileSystemSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="40635-1897">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1897">Property</span></span> | <span data-ttu-id="40635-1898">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1898">Description</span></span> | <span data-ttu-id="40635-1899">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1899">Allowed values</span></span> | <span data-ttu-id="40635-1900">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-1901">recursive</span></span> |<span data-ttu-id="40635-1902">Указывает, следует ли отображать рекурсивный список объектов S3 в каталоге.</span><span class="sxs-lookup"><span data-stu-id="40635-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="40635-1903">True или false</span><span class="sxs-lookup"><span data-stu-id="40635-1903">true/false</span></span> |<span data-ttu-id="40635-1904">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="40635-1905">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1905">Example</span></span>


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

<span data-ttu-id="40635-1906">Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="40635-1907">Файловая система</span><span class="sxs-lookup"><span data-stu-id="40635-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-1908">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-1908">Linked service</span></span>
<span data-ttu-id="40635-1909">Вы можете связать локальную файловую систему с фабрикой данных Azure при помощи связанной службы **локального файлового сервера**.</span><span class="sxs-lookup"><span data-stu-id="40635-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="40635-1910">В таблице ниже приведены описания элементов JSON, которые относятся к связанной службе локального файлового сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="40635-1911">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1911">Property</span></span> | <span data-ttu-id="40635-1912">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1912">Description</span></span> | <span data-ttu-id="40635-1913">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1914">type</span><span class="sxs-lookup"><span data-stu-id="40635-1914">type</span></span> |<span data-ttu-id="40635-1915">Убедитесь, что свойству type присвоено значение **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="40635-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="40635-1916">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1916">Yes</span></span> |
| <span data-ttu-id="40635-1917">host</span><span class="sxs-lookup"><span data-stu-id="40635-1917">host</span></span> |<span data-ttu-id="40635-1918">Задает корневой путь к папке, которую необходимо скопировать.</span><span class="sxs-lookup"><span data-stu-id="40635-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="40635-1919">Чтобы указать специальные знаки в строке, используйте escape-символ "\".</span><span class="sxs-lookup"><span data-stu-id="40635-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40635-1920">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="40635-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="40635-1921">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1921">Yes</span></span> |
| <span data-ttu-id="40635-1922">userid</span><span class="sxs-lookup"><span data-stu-id="40635-1922">userid</span></span> |<span data-ttu-id="40635-1923">Укажите идентификатор пользователя, имеющего доступ к серверу.</span><span class="sxs-lookup"><span data-stu-id="40635-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="40635-1924">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="40635-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="40635-1925">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-1925">password</span></span> |<span data-ttu-id="40635-1926">Укажите пароль для пользователя (userid).</span><span class="sxs-lookup"><span data-stu-id="40635-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="40635-1927">Нет (если выбрать encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="40635-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="40635-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-1928">encryptedCredential</span></span> |<span data-ttu-id="40635-1929">Укажите зашифрованные учетные данные. Чтобы их получить, выполните командлет New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="40635-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="40635-1930">Нет (если имя пользователя и пароль указываются в виде обычного текста)</span><span class="sxs-lookup"><span data-stu-id="40635-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="40635-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-1931">gatewayName</span></span> |<span data-ttu-id="40635-1932">Задает имя шлюза, который следует использовать фабрике данных для подключения к локальному файловому серверу.</span><span class="sxs-lookup"><span data-stu-id="40635-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="40635-1933">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="40635-1934">Пример определений пути к папке</span><span class="sxs-lookup"><span data-stu-id="40635-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="40635-1935">Сценарий</span><span class="sxs-lookup"><span data-stu-id="40635-1935">Scenario</span></span> | <span data-ttu-id="40635-1936">Размещение в определении связанной службы</span><span class="sxs-lookup"><span data-stu-id="40635-1936">Host in linked service definition</span></span> | <span data-ttu-id="40635-1937">Путь к файлу в определении набора данных</span><span class="sxs-lookup"><span data-stu-id="40635-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1938">Локальная папка на компьютере со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="40635-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="40635-1939">Примеры: "D:\\\\*" или "D:\папка\вложенная_папка\\\*"</span><span class="sxs-lookup"><span data-stu-id="40635-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="40635-1940">"D:\\\\" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="40635-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="40635-1941">localhost (для версий, предшествующих версии 2.0 шлюза управления данными)</span><span class="sxs-lookup"><span data-stu-id="40635-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="40635-1942">.\\\\ или "папка\\\\вложенная_папка" (для шлюза управления данными 2.0 и более поздних версий)</span><span class="sxs-lookup"><span data-stu-id="40635-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="40635-1943">"D:\\\\" или "D:\\\\папка\\\\вложенная_папка" (для шлюза версии ниже 2.0)</span><span class="sxs-lookup"><span data-stu-id="40635-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="40635-1944">Удаленная общая папка:</span><span class="sxs-lookup"><span data-stu-id="40635-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="40635-1945">Примеры: "\\\\сервер\\общая_папка\\\*" или "\\\\сервер\\общая_папка\\папка\\вложенная_папка\\*"</span><span class="sxs-lookup"><span data-stu-id="40635-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="40635-1946">\\\\\\\\сервер\\\\общая_папка</span><span class="sxs-lookup"><span data-stu-id="40635-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="40635-1947">.\\\\ или "папка\\\\вложенная_папка"</span><span class="sxs-lookup"><span data-stu-id="40635-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="40635-1948">Пример указания имени пользователя и пароля в виде обычного текста</span><span class="sxs-lookup"><span data-stu-id="40635-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="40635-1949">Пример использования encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="40635-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="40635-1950">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-1951">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-1951">Dataset</span></span>
<span data-ttu-id="40635-1952">Для определения набора данных файловой системы задайте **FileShare** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-1953">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1953">Property</span></span> | <span data-ttu-id="40635-1954">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1954">Description</span></span> | <span data-ttu-id="40635-1955">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="40635-1956">folderPath</span></span> |<span data-ttu-id="40635-1957">Указывает вложенный путь к папке.</span><span class="sxs-lookup"><span data-stu-id="40635-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="40635-1958">Чтобы указать специальные знаки в строке, используйте escape-символ "\".</span><span class="sxs-lookup"><span data-stu-id="40635-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="40635-1959">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="40635-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="40635-1960">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="40635-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40635-1961">Да</span><span class="sxs-lookup"><span data-stu-id="40635-1961">Yes</span></span> |
| <span data-ttu-id="40635-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="40635-1962">fileName</span></span> |<span data-ttu-id="40635-1963">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40635-1964">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40635-1965">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="40635-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="40635-1966">`Data.<Guid>.txt` (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="40635-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="40635-1967">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1967">No</span></span> |
| <span data-ttu-id="40635-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="40635-1968">fileFilter</span></span> |<span data-ttu-id="40635-1969">Укажите фильтр для выбора подмножества файлов из folderPath. Фильтр дает возможность выбирать только некоторые файлы, а не все.</span><span class="sxs-lookup"><span data-stu-id="40635-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="40635-1970">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="40635-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="40635-1971">Пример 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="40635-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="40635-1972">Пример 2: fileFilter: 2016-1-?.txt</span><span class="sxs-lookup"><span data-stu-id="40635-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="40635-1973">Обратите внимание, что свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="40635-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="40635-1974">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1974">No</span></span> |
| <span data-ttu-id="40635-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40635-1975">partitionedBy</span></span> |<span data-ttu-id="40635-1976">С помощью свойства partitionedBy можно указать динамические значения folderPath и fileName для данных временного ряда.</span><span class="sxs-lookup"><span data-stu-id="40635-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="40635-1977">Например, можно параметризовать значение folderPath для каждого часа получения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40635-1978">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1978">No</span></span> |
| <span data-ttu-id="40635-1979">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-1979">format</span></span> | <span data-ttu-id="40635-1980">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-1981">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-1982">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-1983">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-1984">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1984">No</span></span> |
| <span data-ttu-id="40635-1985">compression</span><span class="sxs-lookup"><span data-stu-id="40635-1985">compression</span></span> | <span data-ttu-id="40635-1986">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-1987">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-1988">См. сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-1989">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40635-1990">Свойства filename и fileFilter невозможно использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="40635-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40635-1991">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-1991">Example</span></span>

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

<span data-ttu-id="40635-1992">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40635-1993">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="40635-1994">При копировании данных из файловой системы задайте **FileSystemSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-1995">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-1995">Property</span></span> | <span data-ttu-id="40635-1996">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-1996">Description</span></span> | <span data-ttu-id="40635-1997">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-1997">Allowed values</span></span> | <span data-ttu-id="40635-1998">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-1999">recursive</span></span> |<span data-ttu-id="40635-2000">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="40635-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="40635-2001">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-2001">True, False (default)</span></span> |<span data-ttu-id="40635-2002">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2003">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2003">Example</span></span>

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
<span data-ttu-id="40635-2004">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="40635-2005">Приемник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="40635-2006">При копировании данных в файловую систему задайте **FileSystemSink** в качестве **типа приемника** для действия копирования и задайте в разделе **sink** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="40635-2007">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2007">Property</span></span> | <span data-ttu-id="40635-2008">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2008">Description</span></span> | <span data-ttu-id="40635-2009">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-2009">Allowed values</span></span> | <span data-ttu-id="40635-2010">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="40635-2011">copyBehavior</span></span> |<span data-ttu-id="40635-2012">Это свойство определяет поведение функции копирования, когда в качестве источника используется BlobSource или FileSystem.</span><span class="sxs-lookup"><span data-stu-id="40635-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="40635-2013">/ **PreserveHierarchy:** сохраняет иерархию файлов в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="40635-2014">То есть относительный путь исходного файла в исходной папке идентичен относительному пути целевого файла в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="40635-2015">**FlattenHierarchy**: все файлы из исходной папки создаются на первом уровне в целевой папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="40635-2016">Целевые файлы создаются с автоматически сформированными именами.</span><span class="sxs-lookup"><span data-stu-id="40635-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="40635-2017">**MergeFiles**: объединяет все файлы из исходной папки в один файл.</span><span class="sxs-lookup"><span data-stu-id="40635-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="40635-2018">Если указано имя большого двоичного объекта или имя файла, то оно присваивается объединенному файлу.</span><span class="sxs-lookup"><span data-stu-id="40635-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="40635-2019">В противном случае присваивается автоматически созданное имя файла.</span><span class="sxs-lookup"><span data-stu-id="40635-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="40635-2020">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2020">No</span></span> |
<span data-ttu-id="40635-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="40635-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="40635-2022">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2022">Example</span></span>

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

<span data-ttu-id="40635-2023">Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="40635-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="40635-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-2025">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2025">Linked service</span></span>
<span data-ttu-id="40635-2026">Для определения связанной службы FTP задайте **FtpServer** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2027">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2027">Property</span></span> | <span data-ttu-id="40635-2028">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2028">Description</span></span> | <span data-ttu-id="40635-2029">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2029">Required</span></span> | <span data-ttu-id="40635-2030">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="40635-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2031">host</span><span class="sxs-lookup"><span data-stu-id="40635-2031">host</span></span> |<span data-ttu-id="40635-2032">Имя или IP-адрес FTP-сервера</span><span class="sxs-lookup"><span data-stu-id="40635-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="40635-2033">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="40635-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2034">authenticationType</span></span> |<span data-ttu-id="40635-2035">Укажите тип аутентификации</span><span class="sxs-lookup"><span data-stu-id="40635-2035">Specify authentication type</span></span> |<span data-ttu-id="40635-2036">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2036">Yes</span></span> |<span data-ttu-id="40635-2037">Обычная, анонимная</span><span class="sxs-lookup"><span data-stu-id="40635-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="40635-2038">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2038">username</span></span> |<span data-ttu-id="40635-2039">Пользователь, имеющий доступ к FTP-серверу</span><span class="sxs-lookup"><span data-stu-id="40635-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="40635-2040">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="40635-2041">password</span><span class="sxs-lookup"><span data-stu-id="40635-2041">password</span></span> |<span data-ttu-id="40635-2042">Пароль для пользователя (имя пользователя)</span><span class="sxs-lookup"><span data-stu-id="40635-2042">Password for the user (username)</span></span> |<span data-ttu-id="40635-2043">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="40635-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-2044">encryptedCredential</span></span> |<span data-ttu-id="40635-2045">Зашифрованные учетные данные для доступа к FTP-серверу</span><span class="sxs-lookup"><span data-stu-id="40635-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="40635-2046">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="40635-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2047">gatewayName</span></span> |<span data-ttu-id="40635-2048">Имя шлюза управления данными для подключения к локальному FTP-серверу</span><span class="sxs-lookup"><span data-stu-id="40635-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="40635-2049">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="40635-2050">порт</span><span class="sxs-lookup"><span data-stu-id="40635-2050">port</span></span> |<span data-ttu-id="40635-2051">Порт, прослушиваемый FTP-сервером</span><span class="sxs-lookup"><span data-stu-id="40635-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="40635-2052">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2052">No</span></span> |<span data-ttu-id="40635-2053">21</span><span class="sxs-lookup"><span data-stu-id="40635-2053">21</span></span> |
| <span data-ttu-id="40635-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="40635-2054">enableSsl</span></span> |<span data-ttu-id="40635-2055">Укажите, какой канал следует использовать (FTP через SSL или TLS)</span><span class="sxs-lookup"><span data-stu-id="40635-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="40635-2056">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2056">No</span></span> |<span data-ttu-id="40635-2057">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2057">true</span></span> |
| <span data-ttu-id="40635-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="40635-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="40635-2059">Укажите, следует ли включать проверку SSL-сертификата на сервере при использовании канала FTP через SSL или TLS</span><span class="sxs-lookup"><span data-stu-id="40635-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="40635-2060">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2060">No</span></span> |<span data-ttu-id="40635-2061">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="40635-2062">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="40635-2063">Пример: использование имени пользователя и пароля в виде обычного текста для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="40635-2064">Пример: использование свойств port, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="40635-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="40635-2065">Пример: использование свойства encryptedCredential для проверки подлинности и шлюза</span><span class="sxs-lookup"><span data-stu-id="40635-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="40635-2066">Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-2067">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2067">Dataset</span></span>
<span data-ttu-id="40635-2068">Для определения набора данных FTP задайте **FileShare** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2069">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2069">Property</span></span> | <span data-ttu-id="40635-2070">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2070">Description</span></span> | <span data-ttu-id="40635-2071">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="40635-2072">folderPath</span></span> |<span data-ttu-id="40635-2073">Подпуть к папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2073">Sub path to the folder.</span></span> <span data-ttu-id="40635-2074">Чтобы указать специальные знаки в строке, используйте escape-знак "\".</span><span class="sxs-lookup"><span data-stu-id="40635-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40635-2075">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="40635-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="40635-2076">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="40635-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40635-2077">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2077">Yes</span></span> 
| <span data-ttu-id="40635-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="40635-2078">fileName</span></span> |<span data-ttu-id="40635-2079">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40635-2080">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40635-2081">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="40635-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="40635-2082">Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="40635-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40635-2083">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2083">No</span></span> |
| <span data-ttu-id="40635-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="40635-2084">fileFilter</span></span> |<span data-ttu-id="40635-2085">Укажите фильтр для выбора подмножества файлов из folderPath. Фильтр дает возможность выбирать только некоторые файлы, а не все.</span><span class="sxs-lookup"><span data-stu-id="40635-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="40635-2086">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="40635-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="40635-2087">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="40635-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="40635-2088">Пример 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="40635-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="40635-2089">Свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="40635-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="40635-2090">HDFS не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="40635-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="40635-2091">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2091">No</span></span> |
| <span data-ttu-id="40635-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40635-2092">partitionedBy</span></span> |<span data-ttu-id="40635-2093">Чтобы указать для временного ряда данных динамические путь к папке и имя файла, используйте свойство partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="40635-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="40635-2094">Например, путь к папке folderPath каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="40635-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40635-2095">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2095">No</span></span> |
| <span data-ttu-id="40635-2096">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-2096">format</span></span> | <span data-ttu-id="40635-2097">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-2098">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-2099">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-2100">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-2101">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2101">No</span></span> |
| <span data-ttu-id="40635-2102">compression</span><span class="sxs-lookup"><span data-stu-id="40635-2102">compression</span></span> | <span data-ttu-id="40635-2103">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-2104">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-2105">Узнайте больше о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-2106">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2106">No</span></span> |
| <span data-ttu-id="40635-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="40635-2107">useBinaryTransfer</span></span> |<span data-ttu-id="40635-2108">Укажите, использовать ли режим передачи в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="40635-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="40635-2109">Значение true, если использовать двоичный режим, и false, если ASCII.</span><span class="sxs-lookup"><span data-stu-id="40635-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="40635-2110">Значение по умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="40635-2110">Default value: True.</span></span> <span data-ttu-id="40635-2111">Это свойство можно использовать, только когда тип связанной службы является FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="40635-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="40635-2112">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40635-2113">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="40635-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40635-2114">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
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

<span data-ttu-id="40635-2115">Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40635-2116">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="40635-2117">При копировании данных из FTP задайте **FileSystemSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-2118">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2118">Property</span></span> | <span data-ttu-id="40635-2119">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2119">Description</span></span> | <span data-ttu-id="40635-2120">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-2120">Allowed values</span></span> | <span data-ttu-id="40635-2121">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-2122">recursive</span></span> |<span data-ttu-id="40635-2123">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="40635-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40635-2124">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-2124">True, False (default)</span></span> |<span data-ttu-id="40635-2125">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2126">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2126">Example</span></span>

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

<span data-ttu-id="40635-2127">Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="40635-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="40635-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-2129">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2129">Linked service</span></span>
<span data-ttu-id="40635-2130">Для определения связанной службы HDFS задайте **Hdfs** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2131">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2131">Property</span></span> | <span data-ttu-id="40635-2132">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2132">Description</span></span> | <span data-ttu-id="40635-2133">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2134">type</span><span class="sxs-lookup"><span data-stu-id="40635-2134">type</span></span> |<span data-ttu-id="40635-2135">Для свойства type необходимо задать значение **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="40635-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="40635-2136">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2136">Yes</span></span> |
| <span data-ttu-id="40635-2137">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="40635-2137">Url</span></span> |<span data-ttu-id="40635-2138">URL-адрес в HDFS</span><span class="sxs-lookup"><span data-stu-id="40635-2138">URL to the HDFS</span></span> |<span data-ttu-id="40635-2139">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2139">Yes</span></span> |
| <span data-ttu-id="40635-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2140">authenticationType</span></span> |<span data-ttu-id="40635-2141">Anonymous или Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="40635-2142">Чтобы использовать **аутентификацию Kerberos** для соединителя HDFS, настройте локальную среду, как описано [здесь](#use-kerberos-authentication-for-hdfs-connector).</span><span class="sxs-lookup"><span data-stu-id="40635-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="40635-2143">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2143">Yes</span></span> |
| <span data-ttu-id="40635-2144">userName</span><span class="sxs-lookup"><span data-stu-id="40635-2144">userName</span></span> |<span data-ttu-id="40635-2145">Имя пользователя для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="40635-2146">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="40635-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="40635-2147">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-2147">password</span></span> |<span data-ttu-id="40635-2148">Пароль для проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="40635-2149">Да (для проверки подлинности Windows)</span><span class="sxs-lookup"><span data-stu-id="40635-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="40635-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2150">gatewayName</span></span> |<span data-ttu-id="40635-2151">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной системе HDFS.</span><span class="sxs-lookup"><span data-stu-id="40635-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="40635-2152">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2152">Yes</span></span> |
| <span data-ttu-id="40635-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-2153">encryptedCredential</span></span> |<span data-ttu-id="40635-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) выводит учетные данные доступа.</span><span class="sxs-lookup"><span data-stu-id="40635-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="40635-2155">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="40635-2156">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="40635-2157">Пример: использование проверки подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="40635-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="40635-2158">Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-2159">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2159">Dataset</span></span>
<span data-ttu-id="40635-2160">Для определения набора данных HDFS задайте **FileShare** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2161">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2161">Property</span></span> | <span data-ttu-id="40635-2162">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2162">Description</span></span> | <span data-ttu-id="40635-2163">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="40635-2164">folderPath</span></span> |<span data-ttu-id="40635-2165">Путь к папке,</span><span class="sxs-lookup"><span data-stu-id="40635-2165">Path to the folder.</span></span> <span data-ttu-id="40635-2166">Пример: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="40635-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="40635-2167">Чтобы указать специальные знаки в строке, используйте escape-знак "\".</span><span class="sxs-lookup"><span data-stu-id="40635-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40635-2168">Например, для "папка\вложенная_папка" укажите "папка\\\\вложенная_папка", а для "d:\пример_папки" укажите "d:\\\\пример_папки".</span><span class="sxs-lookup"><span data-stu-id="40635-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="40635-2169">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="40635-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40635-2170">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2170">Yes</span></span> |
| <span data-ttu-id="40635-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="40635-2171">fileName</span></span> |<span data-ttu-id="40635-2172">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40635-2173">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40635-2174">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="40635-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="40635-2175">Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="40635-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40635-2176">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2176">No</span></span> |
| <span data-ttu-id="40635-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40635-2177">partitionedBy</span></span> |<span data-ttu-id="40635-2178">Чтобы указать для временного ряда данных динамические путь к папке и имя файла, используйте свойство partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="40635-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="40635-2179">Например, путь к папке (folderPath) каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="40635-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40635-2180">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2180">No</span></span> |
| <span data-ttu-id="40635-2181">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-2181">format</span></span> | <span data-ttu-id="40635-2182">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-2183">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-2184">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-2185">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-2186">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2186">No</span></span> |
| <span data-ttu-id="40635-2187">compression</span><span class="sxs-lookup"><span data-stu-id="40635-2187">compression</span></span> | <span data-ttu-id="40635-2188">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-2189">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40635-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40635-2190">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-2191">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-2192">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40635-2193">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="40635-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40635-2194">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2194">Example</span></span>

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

<span data-ttu-id="40635-2195">Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40635-2196">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="40635-2197">При копировании данных из HDFS задайте **FileSystemSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="40635-2198">**FileSystemSource** поддерживает следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="40635-2199">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2199">Property</span></span> | <span data-ttu-id="40635-2200">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2200">Description</span></span> | <span data-ttu-id="40635-2201">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-2201">Allowed values</span></span> | <span data-ttu-id="40635-2202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-2203">recursive</span></span> |<span data-ttu-id="40635-2204">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="40635-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40635-2205">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-2205">True, False (default)</span></span> |<span data-ttu-id="40635-2206">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2207">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2207">Example</span></span>

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

<span data-ttu-id="40635-2208">Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="40635-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="40635-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-2210">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2210">Linked service</span></span>
<span data-ttu-id="40635-2211">Для определения связанной службы SFTP задайте **Sftp** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2212">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2212">Property</span></span> | <span data-ttu-id="40635-2213">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2213">Description</span></span> | <span data-ttu-id="40635-2214">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2215">host</span><span class="sxs-lookup"><span data-stu-id="40635-2215">host</span></span> | <span data-ttu-id="40635-2216">Имя или IP-адрес SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="40635-2217">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2217">Yes</span></span> |
| <span data-ttu-id="40635-2218">порт</span><span class="sxs-lookup"><span data-stu-id="40635-2218">port</span></span> |<span data-ttu-id="40635-2219">Порт, прослушиваемый SFTP-сервером.</span><span class="sxs-lookup"><span data-stu-id="40635-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="40635-2220">По умолчанию используется значение 21.</span><span class="sxs-lookup"><span data-stu-id="40635-2220">The default value is: 21</span></span> |<span data-ttu-id="40635-2221">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2221">No</span></span> |
| <span data-ttu-id="40635-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2222">authenticationType</span></span> |<span data-ttu-id="40635-2223">Укажите тип аутентификации.</span><span class="sxs-lookup"><span data-stu-id="40635-2223">Specify authentication type.</span></span> <span data-ttu-id="40635-2224">Допустимые значения: **Basic**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="40635-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="40635-2225">Описание свойств и примеры JSON для каждого типа см. ниже в разделах [использование обычной аутентификации](#using-basic-authentication) и [использование аутентификации с открытым ключом SSH](#using-ssh-public-key-authentication) соответственно.</span><span class="sxs-lookup"><span data-stu-id="40635-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="40635-2226">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2226">Yes</span></span> |
| <span data-ttu-id="40635-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="40635-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="40635-2228">Указывает, нужно ли пропустить проверку ключа узла.</span><span class="sxs-lookup"><span data-stu-id="40635-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="40635-2229">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-2229">No.</span></span> <span data-ttu-id="40635-2230">По умолчанию имеет значение False.</span><span class="sxs-lookup"><span data-stu-id="40635-2230">The default value: false</span></span> |
| <span data-ttu-id="40635-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="40635-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="40635-2232">Содержит отпечаток ключа узла.</span><span class="sxs-lookup"><span data-stu-id="40635-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="40635-2233">Да, если для `skipHostKeyValidation` указано значение False.</span><span class="sxs-lookup"><span data-stu-id="40635-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="40635-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2234">gatewayName</span></span> |<span data-ttu-id="40635-2235">Имя шлюза управления данными для подключения к локальному SFTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="40635-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="40635-2236">Да, если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="40635-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-2237">encryptedCredential</span></span> | <span data-ttu-id="40635-2238">Зашифрованные учетные данные для доступа к SFTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="40635-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="40635-2239">Генерируются автоматически, когда вы выбираете обычную аутентификацию (имя пользователя и пароль) или аутентификацию SshPublicKey (имя пользователя и путь к закрытому ключу или содержимое ключа) в мастере копирования или во всплывающем диалоговом окне ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="40635-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="40635-2240">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-2240">No.</span></span> <span data-ttu-id="40635-2241">Применимо, только если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="40635-2242">Пример: использование обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="40635-2243">Чтобы использовать обычную аутентификацию, задайте для `authenticationType` значение `Basic`, а также все следующие свойства в дополнение к универсальным свойствам соединителя SFTP, которые описаны в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="40635-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="40635-2244">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2244">Property</span></span> | <span data-ttu-id="40635-2245">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2245">Description</span></span> | <span data-ttu-id="40635-2246">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2247">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2247">username</span></span> | <span data-ttu-id="40635-2248">Пользователь, имеющий доступ к SFTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="40635-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="40635-2249">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2249">Yes</span></span> |
| <span data-ttu-id="40635-2250">password</span><span class="sxs-lookup"><span data-stu-id="40635-2250">password</span></span> | <span data-ttu-id="40635-2251">Пароль пользователя, указанного в свойстве имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2251">Password for the user (username).</span></span> | <span data-ttu-id="40635-2252">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="40635-2253">Пример: обычная проверка подлинности с шифрованием учетных данных**</span><span class="sxs-lookup"><span data-stu-id="40635-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="40635-2254">Пример: использование проверки подлинности с открытым ключом SSH**</span><span class="sxs-lookup"><span data-stu-id="40635-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="40635-2255">Чтобы использовать обычную аутентификацию, задайте для `authenticationType` значение `SshPublicKey`, а также все следующие свойства в дополнение к универсальным свойствам соединителя SFTP, которые описаны в последнем разделе.</span><span class="sxs-lookup"><span data-stu-id="40635-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="40635-2256">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2256">Property</span></span> | <span data-ttu-id="40635-2257">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2257">Description</span></span> | <span data-ttu-id="40635-2258">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2259">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2259">username</span></span> |<span data-ttu-id="40635-2260">Пользователь, имеющий доступ к SFTP-серверу.</span><span class="sxs-lookup"><span data-stu-id="40635-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="40635-2261">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2261">Yes</span></span> |
| <span data-ttu-id="40635-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="40635-2262">privateKeyPath</span></span> | <span data-ttu-id="40635-2263">Укажите доступный для шлюза абсолютный путь к файлу закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="40635-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="40635-2264">Должно быть указано одно из свойств: `privateKeyPath` или `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="40635-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="40635-2265">Применимо, только если копирование выполняется с локального SFTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="40635-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="40635-2266">privateKeyContent</span></span> | <span data-ttu-id="40635-2267">Сериализованная строка с содержимым закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="40635-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="40635-2268">Мастер копирования может автоматически считать файл закрытого ключа и извлечь его содержимое.</span><span class="sxs-lookup"><span data-stu-id="40635-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="40635-2269">Если вы используете другие средства и (или) пакет SDK, лучше использовать свойство privateKeyPath.</span><span class="sxs-lookup"><span data-stu-id="40635-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="40635-2270">Должно быть указано одно из свойств: `privateKeyPath` или `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="40635-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="40635-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="40635-2271">passPhrase</span></span> | <span data-ttu-id="40635-2272">Укажите пароль или парольную фразу для расшифровки закрытого ключа, если они используются для защиты файлы ключа.</span><span class="sxs-lookup"><span data-stu-id="40635-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="40635-2273">Да, если файл закрытого ключа защищен парольной фразой.</span><span class="sxs-lookup"><span data-stu-id="40635-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="40635-2274">Пример: проверка подлинности с закрытым ключом SSH, для которого указано содержимое**</span><span class="sxs-lookup"><span data-stu-id="40635-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="40635-2275">Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-2276">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2276">Dataset</span></span>
<span data-ttu-id="40635-2277">Для определения набора данных SFTP задайте **FileShare** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2278">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2278">Property</span></span> | <span data-ttu-id="40635-2279">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2279">Description</span></span> | <span data-ttu-id="40635-2280">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="40635-2281">folderPath</span></span> |<span data-ttu-id="40635-2282">Подпуть к папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2282">Sub path to the folder.</span></span> <span data-ttu-id="40635-2283">Чтобы указать специальные знаки в строке, используйте escape-знак "\".</span><span class="sxs-lookup"><span data-stu-id="40635-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="40635-2284">Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).</span><span class="sxs-lookup"><span data-stu-id="40635-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="40635-2285">Вы можете использовать это свойство вместе с параметром **partitionBy**, чтобы в путях к папкам учитывались дата и время начала и окончания среза.</span><span class="sxs-lookup"><span data-stu-id="40635-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="40635-2286">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2286">Yes</span></span> |
| <span data-ttu-id="40635-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="40635-2287">fileName</span></span> |<span data-ttu-id="40635-2288">Укажите имя файла в папке **folderPath** , если таблица должна ссылаться на определенный файл в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="40635-2289">Если этому свойству не присвоить значение, таблица будет указывать на все файлы в папке.</span><span class="sxs-lookup"><span data-stu-id="40635-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="40635-2290">Если свойство fileName не указано для выходного набора данных, то имя созданного файла будет иметь следующий формат:</span><span class="sxs-lookup"><span data-stu-id="40635-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="40635-2291">Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="40635-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="40635-2292">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2292">No</span></span> |
| <span data-ttu-id="40635-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="40635-2293">fileFilter</span></span> |<span data-ttu-id="40635-2294">Укажите фильтр для выбора подмножества файлов из folderPath. Фильтр дает возможность выбирать только некоторые файлы, а не все.</span><span class="sxs-lookup"><span data-stu-id="40635-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="40635-2295">Допустимые значения: `*` (несколько знаков) и `?` (один знак).</span><span class="sxs-lookup"><span data-stu-id="40635-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="40635-2296">Пример 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="40635-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="40635-2297">Пример 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="40635-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="40635-2298">Свойство fileFilter применяется к входному набору данных FileShare.</span><span class="sxs-lookup"><span data-stu-id="40635-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="40635-2299">HDFS не поддерживает это свойство.</span><span class="sxs-lookup"><span data-stu-id="40635-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="40635-2300">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2300">No</span></span> |
| <span data-ttu-id="40635-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="40635-2301">partitionedBy</span></span> |<span data-ttu-id="40635-2302">Чтобы указать для временного ряда данных динамические путь к папке и имя файла, используйте свойство partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="40635-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="40635-2303">Например, путь к папке folderPath каждый час будет другим.</span><span class="sxs-lookup"><span data-stu-id="40635-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="40635-2304">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2304">No</span></span> |
| <span data-ttu-id="40635-2305">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-2305">format</span></span> | <span data-ttu-id="40635-2306">Поддерживаются следующие типы формата: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-2307">Свойству **type** в разделе format необходимо присвоить одно из этих значений.</span><span class="sxs-lookup"><span data-stu-id="40635-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="40635-2308">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="40635-2309">Если требуется скопировать файлы между файловыми хранилищами **как есть** (двоичное копирование), можно пропустить раздел форматирования в определениях входного и выходного наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="40635-2310">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2310">No</span></span> |
| <span data-ttu-id="40635-2311">compression</span><span class="sxs-lookup"><span data-stu-id="40635-2311">compression</span></span> | <span data-ttu-id="40635-2312">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-2313">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40635-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40635-2314">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-2315">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-2316">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2316">No</span></span> |
| <span data-ttu-id="40635-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="40635-2317">useBinaryTransfer</span></span> |<span data-ttu-id="40635-2318">Укажите, использовать ли режим передачи в двоичном формате.</span><span class="sxs-lookup"><span data-stu-id="40635-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="40635-2319">Значение true, если использовать двоичный режим, и false, если ASCII.</span><span class="sxs-lookup"><span data-stu-id="40635-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="40635-2320">Значение по умолчанию: True.</span><span class="sxs-lookup"><span data-stu-id="40635-2320">Default value: True.</span></span> <span data-ttu-id="40635-2321">Это свойство можно использовать, только когда тип связанной службы является FTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="40635-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="40635-2322">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="40635-2323">Свойства filename и fileFilter нельзя использовать одновременно.</span><span class="sxs-lookup"><span data-stu-id="40635-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="40635-2324">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
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

<span data-ttu-id="40635-2325">Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="40635-2326">Источник файловой системы в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="40635-2327">При копировании данных из источника SFTP задайте **FileSystemSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-2328">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2328">Property</span></span> | <span data-ttu-id="40635-2329">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2329">Description</span></span> | <span data-ttu-id="40635-2330">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-2330">Allowed values</span></span> | <span data-ttu-id="40635-2331">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="40635-2332">recursive</span></span> |<span data-ttu-id="40635-2333">Указывает, следует ли читать данные рекурсивно из вложенных папок или только из указанной папки.</span><span class="sxs-lookup"><span data-stu-id="40635-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="40635-2334">True, False (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-2334">True, False (default)</span></span> |<span data-ttu-id="40635-2335">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="40635-2336">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2336">Example</span></span>

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

<span data-ttu-id="40635-2337">Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="40635-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="40635-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-2339">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2339">Linked service</span></span>
<span data-ttu-id="40635-2340">Для определения связанной службы HTTP задайте **Http** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2341">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2341">Property</span></span> | <span data-ttu-id="40635-2342">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2342">Description</span></span> | <span data-ttu-id="40635-2343">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2344">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="40635-2344">url</span></span> | <span data-ttu-id="40635-2345">Базовый URL-адрес веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="40635-2346">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2346">Yes</span></span> |
| <span data-ttu-id="40635-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2347">authenticationType</span></span> | <span data-ttu-id="40635-2348">Указывает тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="40635-2348">Specifies the authentication type.</span></span> <span data-ttu-id="40635-2349">Допустимые значения: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="40635-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="40635-2350">В разделах ниже описываются дополнительные свойства и приведены примеры JSON для поддерживаемых типов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="40635-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="40635-2351">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2351">Yes</span></span> |
| <span data-ttu-id="40635-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="40635-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="40635-2353">Укажите, следует ли включать проверку SSL-сертификата на сервере, если источником является веб-сервер HTTPS.</span><span class="sxs-lookup"><span data-stu-id="40635-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="40635-2354">Нет. Значение по умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="40635-2354">No, default is true</span></span> |
| <span data-ttu-id="40635-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2355">gatewayName</span></span> | <span data-ttu-id="40635-2356">Имя шлюза управления данными для подключения к локальному источнику HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="40635-2357">Да, если копирование выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="40635-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-2358">encryptedCredential</span></span> | <span data-ttu-id="40635-2359">Зашифрованные учетные данные для доступа к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="40635-2360">При настройке сведений для проверки подлинности в мастере копирования или всплывающем диалоговом окне ClickOnce создаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="40635-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="40635-2361">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-2361">No.</span></span> <span data-ttu-id="40635-2362">Применимо, только когда копирование данных выполняется с локального HTTP-сервера.</span><span class="sxs-lookup"><span data-stu-id="40635-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="40635-2363">Пример: использование типов проверки подлинности Basic, Digest или Windows</span><span class="sxs-lookup"><span data-stu-id="40635-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="40635-2364">Задайте для свойства `authenticationType` значения `Basic`, `Digest` или `Windows` и укажите следующие свойства помимо универсальных свойств соединителя HTTP, приведенных выше.</span><span class="sxs-lookup"><span data-stu-id="40635-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="40635-2365">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2365">Property</span></span> | <span data-ttu-id="40635-2366">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2366">Description</span></span> | <span data-ttu-id="40635-2367">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2368">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2368">username</span></span> | <span data-ttu-id="40635-2369">Имя пользователя для доступа к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="40635-2370">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2370">Yes</span></span> |
| <span data-ttu-id="40635-2371">password</span><span class="sxs-lookup"><span data-stu-id="40635-2371">password</span></span> | <span data-ttu-id="40635-2372">Пароль пользователя, указанного в свойстве имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2372">Password for the user (username).</span></span> | <span data-ttu-id="40635-2373">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="40635-2374">Пример: использование типа проверки подлинности ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="40635-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="40635-2375">Чтобы использовать базовую проверку подлинности, задайте для `authenticationType` значение `ClientCertificate` и укажите приведенные ниже свойства помимо универсальных свойств соединителя HTTP, которые описаны выше.</span><span class="sxs-lookup"><span data-stu-id="40635-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="40635-2376">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2376">Property</span></span> | <span data-ttu-id="40635-2377">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2377">Description</span></span> | <span data-ttu-id="40635-2378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="40635-2379">embeddedCertData</span></span> | <span data-ttu-id="40635-2380">Содержимое двоичных данных файла обмена личной информацией (PFX-файла) с кодировкой Base64.</span><span class="sxs-lookup"><span data-stu-id="40635-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="40635-2381">Должно быть указано одно из свойств: `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="40635-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="40635-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="40635-2382">certThumbprint</span></span> | <span data-ttu-id="40635-2383">Отпечаток сертификата, который был установлен в хранилище сертификатов на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="40635-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="40635-2384">Применимо, только когда копирование данных выполняется из локального источника HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="40635-2385">Должно быть указано одно из свойств: `embeddedCertData` или `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="40635-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="40635-2386">password</span><span class="sxs-lookup"><span data-stu-id="40635-2386">password</span></span> | <span data-ttu-id="40635-2387">Пароль, связанный с сертификатом.</span><span class="sxs-lookup"><span data-stu-id="40635-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="40635-2388">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2388">No</span></span> |

<span data-ttu-id="40635-2389">Если вы используете свойство `certThumbprint` для проверки подлинности, а сертификат установлен в личном хранилище локального компьютера, вам необходимо предоставить службе шлюза разрешение на чтение.</span><span class="sxs-lookup"><span data-stu-id="40635-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="40635-2390">Запустите консоль управления (MMC).</span><span class="sxs-lookup"><span data-stu-id="40635-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="40635-2391">Добавьте оснастку **Сертификаты**, которая связана с **локальным компьютером**.</span><span class="sxs-lookup"><span data-stu-id="40635-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="40635-2392">Разверните **Сертификаты**, **Личные**, а затем щелкните **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="40635-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="40635-2393">Щелкните правой кнопкой мыши сертификат в личном хранилище, а затем выберите **Все задачи**->**Управление закрытыми ключами...**</span><span class="sxs-lookup"><span data-stu-id="40635-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="40635-2394">На вкладке **Безопасность** добавьте учетную запись пользователя, под которой запущена служба узла шлюза управления данными с доступом на чтение к сертификату.</span><span class="sxs-lookup"><span data-stu-id="40635-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="40635-2395">**Пример: использование клиентского сертификата.**Эта связанная служба связывает фабрику данных с локальным веб-сервером HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="40635-2396">Она использует сертификат клиента, установленный на компьютере со шлюзом управления данными.</span><span class="sxs-lookup"><span data-stu-id="40635-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="40635-2397">Пример: использование сертификата клиента в файле</span><span class="sxs-lookup"><span data-stu-id="40635-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="40635-2398">Эта связанная служба связывает фабрику данных с локальным веб-сервером HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="40635-2399">Она использует файл сертификата клиента на компьютере, где установлен шлюз управления данными.</span><span class="sxs-lookup"><span data-stu-id="40635-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="40635-2400">Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-2401">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2401">Dataset</span></span>
<span data-ttu-id="40635-2402">Для определения набора данных HTTP задайте **Http** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2403">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2403">Property</span></span> | <span data-ttu-id="40635-2404">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2404">Description</span></span> | <span data-ttu-id="40635-2405">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="40635-2406">relativeUrl</span></span> | <span data-ttu-id="40635-2407">Относительный URL-адрес ресурса, который содержит данные.</span><span class="sxs-lookup"><span data-stu-id="40635-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="40635-2408">Если путь не задан, используется только URL-адрес, указанный в определении связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="40635-2409">Для создания динамического URL-адреса можно использовать [функции фабрики данных и системные переменные](data-factory-functions-variables.md), например: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span><span class="sxs-lookup"><span data-stu-id="40635-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="40635-2410">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2410">No</span></span> |
| <span data-ttu-id="40635-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="40635-2411">requestMethod</span></span> | <span data-ttu-id="40635-2412">Метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="40635-2412">Http method.</span></span> <span data-ttu-id="40635-2413">Допустимые значения: **GET** или **POST**.</span><span class="sxs-lookup"><span data-stu-id="40635-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="40635-2414">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-2414">No.</span></span> <span data-ttu-id="40635-2415">Значение по умолчанию — `GET`.</span><span class="sxs-lookup"><span data-stu-id="40635-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="40635-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="40635-2416">additionalHeaders</span></span> | <span data-ttu-id="40635-2417">Дополнительные заголовки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="40635-2418">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2418">No</span></span> |
| <span data-ttu-id="40635-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="40635-2419">requestBody</span></span> | <span data-ttu-id="40635-2420">Текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-2420">Body for HTTP request.</span></span> | <span data-ttu-id="40635-2421">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2421">No</span></span> |
| <span data-ttu-id="40635-2422">свойства</span><span class="sxs-lookup"><span data-stu-id="40635-2422">format</span></span> | <span data-ttu-id="40635-2423">Если вы хотите просто **извлечь данные из конечной точки HTTP "как есть"** — без анализа, пропустите параметры форматирования.</span><span class="sxs-lookup"><span data-stu-id="40635-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="40635-2424">Поддерживаемые форматы для выполнения анализа содержимого ответа HTTP в процессе выполнения операции копирования: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** и **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="40635-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="40635-2425">Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="40635-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="40635-2426">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2426">No</span></span> |
| <span data-ttu-id="40635-2427">compression</span><span class="sxs-lookup"><span data-stu-id="40635-2427">compression</span></span> | <span data-ttu-id="40635-2428">Укажите тип и уровень сжатия данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="40635-2429">Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="40635-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="40635-2430">Поддерживаемые уровни: **Optimal** и **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="40635-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="40635-2431">См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="40635-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="40635-2432">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="40635-2433">Пример: использование метода GET (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="40635-2433">Example: using the GET (default) method</span></span>

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

#### <a name="example-using-the-post-method"></a><span data-ttu-id="40635-2434">Пример: использование метода POST</span><span class="sxs-lookup"><span data-stu-id="40635-2434">Example: using the POST method</span></span>

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
<span data-ttu-id="40635-2435">Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="40635-2436">Источник HTTP в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="40635-2437">При копировании данных из источника HTTP задайте **HttpSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-2438">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2438">Property</span></span> | <span data-ttu-id="40635-2439">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2439">Description</span></span> | <span data-ttu-id="40635-2440">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40635-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="40635-2441">httpRequestTimeout</span></span> | <span data-ttu-id="40635-2442">Время ожидания ответа для HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="40635-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="40635-2443">Это интервал времени для получения ответа, а не считывания данных ответа.</span><span class="sxs-lookup"><span data-stu-id="40635-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="40635-2444">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-2444">No.</span></span> <span data-ttu-id="40635-2445">Значение по умолчанию  — 00:01:40.</span><span class="sxs-lookup"><span data-stu-id="40635-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="40635-2446">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
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

<span data-ttu-id="40635-2447">Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="40635-2448">OData</span><span class="sxs-lookup"><span data-stu-id="40635-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-2449">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2449">Linked service</span></span>
<span data-ttu-id="40635-2450">Для определения связанной службы OData задайте **OData** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2451">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2451">Property</span></span> | <span data-ttu-id="40635-2452">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2452">Description</span></span> | <span data-ttu-id="40635-2453">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2454">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="40635-2454">url</span></span> |<span data-ttu-id="40635-2455">URL-адрес службы OData.</span><span class="sxs-lookup"><span data-stu-id="40635-2455">Url of the OData service.</span></span> |<span data-ttu-id="40635-2456">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2456">Yes</span></span> |
| <span data-ttu-id="40635-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2457">authenticationType</span></span> |<span data-ttu-id="40635-2458">Тип проверки подлинности, используемый для подключения к источнику OData.</span><span class="sxs-lookup"><span data-stu-id="40635-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="40635-2459">Возможные значения для облачной службы OData: "Анонимно", "Обычная" и "OAuth" (обратите внимание, что сейчас фабрика данных Azure поддерживает только аутентификацию OAuth на основе Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="40635-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="40635-2460">Для локальной службы OData возможными значениями являются "Анонимная", "Обычная" и "Windows".</span><span class="sxs-lookup"><span data-stu-id="40635-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="40635-2461">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2461">Yes</span></span> |
| <span data-ttu-id="40635-2462">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2462">username</span></span> |<span data-ttu-id="40635-2463">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="40635-2464">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="40635-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="40635-2465">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-2465">password</span></span> |<span data-ttu-id="40635-2466">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-2467">Да (только при использовании обычной проверки подлинности)</span><span class="sxs-lookup"><span data-stu-id="40635-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="40635-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="40635-2468">authorizedCredential</span></span> |<span data-ttu-id="40635-2469">Если используется OAuth, в мастере копирования фабрики данных или редакторе нажмите кнопку **Авторизовать** и введите свои учетные данные, после чего значение этого свойства будет создано автоматически.</span><span class="sxs-lookup"><span data-stu-id="40635-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="40635-2470">Да (только при использовании аутентификации OAuth)</span><span class="sxs-lookup"><span data-stu-id="40635-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="40635-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2471">gatewayName</span></span> |<span data-ttu-id="40635-2472">Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной службе OData.</span><span class="sxs-lookup"><span data-stu-id="40635-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="40635-2473">Его необходимо указывать только в том случае, если вы копируете данные из источника в локальной службе OData.</span><span class="sxs-lookup"><span data-stu-id="40635-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="40635-2474">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="40635-2475">Пример: использование обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="40635-2476">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="40635-2477">Пример: использование проверки подлинности Windows при получении доступа к локальному источнику OData</span><span class="sxs-lookup"><span data-stu-id="40635-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="40635-2478">Пример: использование проверки подлинности OAuth при получении доступа к облачному источнику OData</span><span class="sxs-lookup"><span data-stu-id="40635-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="40635-2479">Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="40635-2480">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2480">Dataset</span></span>
<span data-ttu-id="40635-2481">Для определения набора данных OData задайте **ODataResource** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2482">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2482">Property</span></span> | <span data-ttu-id="40635-2483">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2483">Description</span></span> | <span data-ttu-id="40635-2484">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2485">path</span><span class="sxs-lookup"><span data-stu-id="40635-2485">path</span></span> |<span data-ttu-id="40635-2486">Путь к ресурсу OData</span><span class="sxs-lookup"><span data-stu-id="40635-2486">Path to the OData resource</span></span> |<span data-ttu-id="40635-2487">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2488">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2488">Example</span></span>

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

<span data-ttu-id="40635-2489">Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-2490">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-2491">При копировании данных из источника OData задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-2492">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2492">Property</span></span> | <span data-ttu-id="40635-2493">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2493">Description</span></span> | <span data-ttu-id="40635-2494">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2494">Example</span></span> | <span data-ttu-id="40635-2495">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2496">query</span><span class="sxs-lookup"><span data-stu-id="40635-2496">query</span></span> |<span data-ttu-id="40635-2497">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="40635-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="40635-2499">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2500">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2500">Example</span></span>

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

<span data-ttu-id="40635-2501">Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="40635-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="40635-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-2503">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2503">Linked service</span></span>
<span data-ttu-id="40635-2504">Для определения связанной службы ODBC задайте **OnPremisesOdbc** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2505">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2505">Property</span></span> | <span data-ttu-id="40635-2506">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2506">Description</span></span> | <span data-ttu-id="40635-2507">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-2508">connectionString</span></span> |<span data-ttu-id="40635-2509">Учетные данные в строке подключения, не используемые для получения доступа, а также дополнительные зашифрованные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="40635-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="40635-2510">Примеры приведены в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="40635-2510">See examples in the following sections.</span></span> |<span data-ttu-id="40635-2511">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2511">Yes</span></span> |
| <span data-ttu-id="40635-2512">credential</span><span class="sxs-lookup"><span data-stu-id="40635-2512">credential</span></span> |<span data-ttu-id="40635-2513">Учетные данные в строке подключения, используемые для получения доступа и указанные в формате "драйвер-определенное свойство-значение".</span><span class="sxs-lookup"><span data-stu-id="40635-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="40635-2514">Пример: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="40635-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="40635-2515">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2515">No</span></span> |
| <span data-ttu-id="40635-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2516">authenticationType</span></span> |<span data-ttu-id="40635-2517">Тип проверки подлинности, используемый для подключения к хранилищу данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="40635-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="40635-2518">Возможными значениями являются: "Анонимная" и "Обычная".</span><span class="sxs-lookup"><span data-stu-id="40635-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="40635-2519">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2519">Yes</span></span> |
| <span data-ttu-id="40635-2520">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2520">username</span></span> |<span data-ttu-id="40635-2521">При использовании обычной проверки подлинности укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="40635-2522">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2522">No</span></span> |
| <span data-ttu-id="40635-2523">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-2523">password</span></span> |<span data-ttu-id="40635-2524">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-2525">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2525">No</span></span> |
| <span data-ttu-id="40635-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2526">gatewayName</span></span> |<span data-ttu-id="40635-2527">Имя шлюза, который следует использовать службе фабрики данных для подключения к хранилищу данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="40635-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="40635-2528">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="40635-2529">Пример: использование обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="40635-2530">Пример: использование обычной проверки подлинности и шифрования учетных данных</span><span class="sxs-lookup"><span data-stu-id="40635-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="40635-2531">Учетные данные можно зашифровать с помощью командлета [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0) или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (Azure PowerShell 0.9 или более ранней версии).</span><span class="sxs-lookup"><span data-stu-id="40635-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="40635-2532">Пример: использование анонимной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="40635-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="40635-2533">Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-2534">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2534">Dataset</span></span>
<span data-ttu-id="40635-2535">Для определения набора данных ODBC задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2536">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2536">Property</span></span> | <span data-ttu-id="40635-2537">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2537">Description</span></span> | <span data-ttu-id="40635-2538">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-2539">tableName</span></span> |<span data-ttu-id="40635-2540">Имя таблицы в хранилище данных ODBC.</span><span class="sxs-lookup"><span data-stu-id="40635-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="40635-2541">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="40635-2542">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2542">Example</span></span>

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

<span data-ttu-id="40635-2543">Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-2544">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-2545">При копировании данных из хранилища данных ODBC задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-2546">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2546">Property</span></span> | <span data-ttu-id="40635-2547">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2547">Description</span></span> | <span data-ttu-id="40635-2548">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-2548">Allowed values</span></span> | <span data-ttu-id="40635-2549">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2550">query</span><span class="sxs-lookup"><span data-stu-id="40635-2550">query</span></span> |<span data-ttu-id="40635-2551">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-2552">Строка запроса SQL.</span><span class="sxs-lookup"><span data-stu-id="40635-2552">SQL query string.</span></span> <span data-ttu-id="40635-2553">Например, `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="40635-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="40635-2554">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2555">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2555">Example</span></span>

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

<span data-ttu-id="40635-2556">Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="40635-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="40635-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="40635-2558">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2558">Linked service</span></span>
<span data-ttu-id="40635-2559">Для определения связанной службы Salesforce задайте **Salesforce** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2560">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2560">Property</span></span> | <span data-ttu-id="40635-2561">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2561">Description</span></span> | <span data-ttu-id="40635-2562">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="40635-2563">environmentUrl</span></span> | <span data-ttu-id="40635-2564">Укажите URL-адрес экземпляра Salesforce.</span><span class="sxs-lookup"><span data-stu-id="40635-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="40635-2565">— URL-адрес по умолчанию — https://login.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="40635-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="40635-2566">— Чтобы скопировать данные из песочницы, укажите URL-адрес https://test.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="40635-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="40635-2567">— Чтобы скопировать данные из пользовательского домена, укажите URL-адрес, например https://[домен].my.salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="40635-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="40635-2568">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2568">No</span></span> |
| <span data-ttu-id="40635-2569">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2569">username</span></span> |<span data-ttu-id="40635-2570">Укажите имя пользователя для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="40635-2571">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2571">Yes</span></span> |
| <span data-ttu-id="40635-2572">password</span><span class="sxs-lookup"><span data-stu-id="40635-2572">password</span></span> |<span data-ttu-id="40635-2573">Укажите пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="40635-2574">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2574">Yes</span></span> |
| <span data-ttu-id="40635-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="40635-2575">securityToken</span></span> |<span data-ttu-id="40635-2576">Укажите маркер безопасности для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="40635-2577">Инструкции по получению и сбросу маркера безопасности см. в статье [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) (Получение маркера безопасности).</span><span class="sxs-lookup"><span data-stu-id="40635-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="40635-2578">Общие сведения о маркере безопасности см. в статье [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm) (Безопасность и API).</span><span class="sxs-lookup"><span data-stu-id="40635-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="40635-2579">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2580">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2580">Example</span></span>

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

<span data-ttu-id="40635-2581">Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-2582">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2582">Dataset</span></span>
<span data-ttu-id="40635-2583">Для определения набора данных Salesforce задайте **RelationalTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2584">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2584">Property</span></span> | <span data-ttu-id="40635-2585">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2585">Description</span></span> | <span data-ttu-id="40635-2586">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="40635-2587">tableName</span></span> |<span data-ttu-id="40635-2588">Имя таблицы в Salesforce</span><span class="sxs-lookup"><span data-stu-id="40635-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="40635-2589">Нет (если для свойства **RelationalSource** задано значение **query**).</span><span class="sxs-lookup"><span data-stu-id="40635-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2590">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2590">Example</span></span>

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

<span data-ttu-id="40635-2591">Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="40635-2592">Реляционный источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="40635-2593">При копировании данных из Salesforce задайте **RelationalSource** в качестве **типа источника** для действия копирования и укажите в разделе **source** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="40635-2594">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2594">Property</span></span> | <span data-ttu-id="40635-2595">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2595">Description</span></span> | <span data-ttu-id="40635-2596">Допустимые значения</span><span class="sxs-lookup"><span data-stu-id="40635-2596">Allowed values</span></span> | <span data-ttu-id="40635-2597">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="40635-2598">query</span><span class="sxs-lookup"><span data-stu-id="40635-2598">query</span></span> |<span data-ttu-id="40635-2599">Используйте пользовательский запрос для чтения данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="40635-2600">Запрос SQL-92 или запрос, написанный на [объектно-ориентированном языке запросов Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) .</span><span class="sxs-lookup"><span data-stu-id="40635-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="40635-2601">Пример: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="40635-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="40635-2602">Нет (если для свойства **tableName** задано значение **dataset**).</span><span class="sxs-lookup"><span data-stu-id="40635-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2603">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
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
> <span data-ttu-id="40635-2604">Имя API для любых настраиваемых объектов должно содержать приставку __c.</span><span class="sxs-lookup"><span data-stu-id="40635-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="40635-2605">Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="40635-2606">Веб-данные</span><span class="sxs-lookup"><span data-stu-id="40635-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2607">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2607">Linked service</span></span>
<span data-ttu-id="40635-2608">Для определения связанной веб-службы задайте **Web** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2609">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2609">Property</span></span> | <span data-ttu-id="40635-2610">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2610">Description</span></span> | <span data-ttu-id="40635-2611">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2612">URL-адрес</span><span class="sxs-lookup"><span data-stu-id="40635-2612">Url</span></span> |<span data-ttu-id="40635-2613">URL-адрес источника Web</span><span class="sxs-lookup"><span data-stu-id="40635-2613">URL to the Web source</span></span> |<span data-ttu-id="40635-2614">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2614">Yes</span></span> |
| <span data-ttu-id="40635-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="40635-2615">authenticationType</span></span> |<span data-ttu-id="40635-2616">Анонимная.</span><span class="sxs-lookup"><span data-stu-id="40635-2616">Anonymous.</span></span> |<span data-ttu-id="40635-2617">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="40635-2618">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2618">Example</span></span>


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

<span data-ttu-id="40635-2619">Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="40635-2620">Выборка</span><span class="sxs-lookup"><span data-stu-id="40635-2620">Dataset</span></span>
<span data-ttu-id="40635-2621">Для определения веб-набора данных задайте **WebTable** в качестве **типа** набора данных и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="40635-2622">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2622">Property</span></span> | <span data-ttu-id="40635-2623">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2623">Description</span></span> | <span data-ttu-id="40635-2624">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-2625">type</span><span class="sxs-lookup"><span data-stu-id="40635-2625">type</span></span> |<span data-ttu-id="40635-2626">Тип набора данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2626">type of the dataset.</span></span> <span data-ttu-id="40635-2627">Необходимо задать значение **WebTable**</span><span class="sxs-lookup"><span data-stu-id="40635-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="40635-2628">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2628">Yes</span></span> |
| <span data-ttu-id="40635-2629">path</span><span class="sxs-lookup"><span data-stu-id="40635-2629">path</span></span> |<span data-ttu-id="40635-2630">Относительный URL-адрес ресурса, который содержит таблицу.</span><span class="sxs-lookup"><span data-stu-id="40635-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="40635-2631">Нет.</span><span class="sxs-lookup"><span data-stu-id="40635-2631">No.</span></span> <span data-ttu-id="40635-2632">Если путь не задан, используется только URL-адрес, указанный в определении связанной службы.</span><span class="sxs-lookup"><span data-stu-id="40635-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="40635-2633">index</span><span class="sxs-lookup"><span data-stu-id="40635-2633">index</span></span> |<span data-ttu-id="40635-2634">Индекс таблицы в ресурсе.</span><span class="sxs-lookup"><span data-stu-id="40635-2634">The index of the table in the resource.</span></span> <span data-ttu-id="40635-2635">Дополнительные сведения см. в разделе [Получение индекса таблицы на HTML-странице](#get-index-of-a-table-in-an-html-page).</span><span class="sxs-lookup"><span data-stu-id="40635-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="40635-2636">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="40635-2637">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2637">Example</span></span>

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

<span data-ttu-id="40635-2638">Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="40635-2639">Веб-источник в действии копирования</span><span class="sxs-lookup"><span data-stu-id="40635-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="40635-2640">При копировании данных из веб-таблицы задайте **WebSource** в качестве **типа источника** для действия копирования.</span><span class="sxs-lookup"><span data-stu-id="40635-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="40635-2641">В настоящее время, если источник в действии копирования относится к типу **WebSource**, дополнительные свойства не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="40635-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="40635-2642">Пример</span><span class="sxs-lookup"><span data-stu-id="40635-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
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

<span data-ttu-id="40635-2643">Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="40635-2644">ВЫЧИСЛИТЕЛЬНЫЕ СРЕДЫ</span><span class="sxs-lookup"><span data-stu-id="40635-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="40635-2645">Следующая таблица содержит список вычислительных сред, поддерживаемых фабрикой данных, и доступных в них действий преобразования.</span><span class="sxs-lookup"><span data-stu-id="40635-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="40635-2646">Щелкните ссылку для интересующего вас вычисления, чтобы просмотреть схемы JSON связанной службы и связать ее с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="40635-2647">Вычислительная среда</span><span class="sxs-lookup"><span data-stu-id="40635-2647">Compute environment</span></span> | <span data-ttu-id="40635-2648">Действия</span><span class="sxs-lookup"><span data-stu-id="40635-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="40635-2649">[Кластер HDInsight по запросу](#on-demand-azure-hdinsight-cluster) или [собственный кластер HDInsight](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="40635-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="40635-2650">[Настраиваемое действие .NET](#net-custom-activity), [действие Hive](#hdinsight-hive-activity), [действие Pig] (#hdinsight-pig-activity), [действие MapReduce](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [действие Spark](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="40635-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="40635-2651">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="40635-2652">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="40635-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="40635-2653">машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="40635-2654">[Действие выполнения пакета в службе машинного обучения](#machine-learning-batch-execution-activity), [действие обновления ресурса в службе машинного обучения](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="40635-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="40635-2655">Аналитика озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="40635-2656">Аналитика озера данных U-SQL</span><span class="sxs-lookup"><span data-stu-id="40635-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="40635-2657">[База данных Azure SQL](#azure-sql-database-1), [хранилище данных Azure SQL](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="40635-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="40635-2658">Хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="40635-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="40635-2659">Кластер Azure HDInsight по требованию</span><span class="sxs-lookup"><span data-stu-id="40635-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="40635-2660">Для обработки данных служба фабрики данных Azure автоматически создает кластер HDInsight под управлением Windows/Linux по запросу.</span><span class="sxs-lookup"><span data-stu-id="40635-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="40635-2661">Кластер создается в том же регионе, что и учетная запись хранения (свойство linkedServiceName в JSON), связанная с кластером.</span><span class="sxs-lookup"><span data-stu-id="40635-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="40635-2662">В этой связанной службе можно выполнить следующие действия преобразования: [настраиваемое действие .NET](#net-custom-activity), [действие Hive](#hdinsight-hive-activity), [действие Pig] (#hdinsight-pig-activity), [действие MapReduce](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [действие Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="40635-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2663">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2663">Linked service</span></span> 
<span data-ttu-id="40635-2664">Следующая таблица содержит описание свойств, используемых в определении Azure JSON связанной службы HDInsight по требованию.</span><span class="sxs-lookup"><span data-stu-id="40635-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="40635-2665">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2665">Property</span></span> | <span data-ttu-id="40635-2666">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2666">Description</span></span> | <span data-ttu-id="40635-2667">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2668">type</span><span class="sxs-lookup"><span data-stu-id="40635-2668">type</span></span> |<span data-ttu-id="40635-2669">Свойству type необходимо присвоить значение **HDInsightOnDemand**.</span><span class="sxs-lookup"><span data-stu-id="40635-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="40635-2670">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2670">Yes</span></span> |
| <span data-ttu-id="40635-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="40635-2671">clusterSize</span></span> |<span data-ttu-id="40635-2672">Общее количество рабочих узлов и узлов данных в кластере.</span><span class="sxs-lookup"><span data-stu-id="40635-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="40635-2673">Кластер HDInsight создается с 2 головными узлами и количеством рабочих узлов, заданным в этом свойстве.</span><span class="sxs-lookup"><span data-stu-id="40635-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="40635-2674">Узлы имеют размер Standard_D3 с 4 ядрами, то есть кластер с 4 рабочими узлами использует 24 ядра (4\*4 = 16 для рабочих узлов + 2\*4 = 8 для головных узлов).</span><span class="sxs-lookup"><span data-stu-id="40635-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="40635-2675">Дополнительные сведения об уровне Standard_D3 см. в статье [Создание кластеров Hadoop под управлением Linux в HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="40635-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="40635-2676">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2676">Yes</span></span> |
| <span data-ttu-id="40635-2677">timeToLive</span><span class="sxs-lookup"><span data-stu-id="40635-2677">timetolive</span></span> |<span data-ttu-id="40635-2678">Допустимое время простоя кластера HDInsight по запросу.</span><span class="sxs-lookup"><span data-stu-id="40635-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="40635-2679">Указывает, как долго кластер HDInsight по запросу остается активным после выполнения действия, если в кластере нет других активных заданий.</span><span class="sxs-lookup"><span data-stu-id="40635-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="40635-2680">Например, если выполнение действия занимает 6 минут, а значение свойства timetolive равно 5 минутам, кластер остается активным в течение 5 минут по истечении 6-минутного выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="40635-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="40635-2681">Если в течение этих 6 минут выполняется другое действие, оно обрабатывается в том же кластере.</span><span class="sxs-lookup"><span data-stu-id="40635-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="40635-2682">Создание кластера HDInsight по запросу является ресурсоемкой операцией и может занять некоторое время. При необходимости используйте этот параметр для повышения производительности фабрики данных путем повторного использования кластера HDInsight по запросу.</span><span class="sxs-lookup"><span data-stu-id="40635-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="40635-2683">Если значение timetolive равно 0, кластер удаляется сразу после выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="40635-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="40635-2684">С другой стороны, если задать большое значение, кластер может простаивать без необходимости, что приведет к большим затратам.</span><span class="sxs-lookup"><span data-stu-id="40635-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="40635-2685">Поэтому необходимо установить соответствующее значение в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="40635-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="40635-2686">Если значение свойства timetolive задано правильно, один и тот же экземпляр кластера HDInsight по запросу могут совместно использовать несколько конвейеров.</span><span class="sxs-lookup"><span data-stu-id="40635-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="40635-2687">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2687">Yes</span></span> |
| <span data-ttu-id="40635-2688">версия</span><span class="sxs-lookup"><span data-stu-id="40635-2688">version</span></span> |<span data-ttu-id="40635-2689">Версия кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="40635-2690">Подробные сведения см. в статье [Версии HDInsight, поддерживаемые в фабрике данных Azure](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="40635-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="40635-2691">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2691">No</span></span> |
| <span data-ttu-id="40635-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40635-2692">linkedServiceName</span></span> |<span data-ttu-id="40635-2693">Связанная служба хранилища Azure, которую кластер по запросу должен использовать для хранения и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="40635-2694">В настоящее время недоступно создание кластера HDInsight по запросу, который использует в качестве хранилища Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40635-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="40635-2695">Чтобы сохранить данные результатов обработки HDInsight в Azure Data Lake Store, воспользуйтесь действием копирования и скопируйте данные из хранилища BLOB-объектов Azure в Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40635-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="40635-2696">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2696">Yes</span></span> |
| <span data-ttu-id="40635-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="40635-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="40635-2698">Указывает дополнительные учетные записи хранения для связанной службы HDInsight, чтобы служба фабрики данных могла регистрировать их от вашего имени.</span><span class="sxs-lookup"><span data-stu-id="40635-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="40635-2699">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2699">No</span></span> |
| <span data-ttu-id="40635-2700">osType</span><span class="sxs-lookup"><span data-stu-id="40635-2700">osType</span></span> |<span data-ttu-id="40635-2701">Тип операционной системы.</span><span class="sxs-lookup"><span data-stu-id="40635-2701">Type of operating system.</span></span> <span data-ttu-id="40635-2702">Допустимые значения: Windows (по умолчанию) и Linux.</span><span class="sxs-lookup"><span data-stu-id="40635-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="40635-2703">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2703">No</span></span> |
| <span data-ttu-id="40635-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40635-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="40635-2705">Имя связанной службы SQL Azure, указывающие на базу данных HCatalog.</span><span class="sxs-lookup"><span data-stu-id="40635-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="40635-2706">При создании кластера HDInsight по запросу используется база данных SQL Azure в качестве хранилища метаданных.</span><span class="sxs-lookup"><span data-stu-id="40635-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="40635-2707">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="40635-2708">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2708">JSON example</span></span>
<span data-ttu-id="40635-2709">Представленный ниже код JSON определяет связанную службу HDInsight по запросу под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="40635-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="40635-2710">При обработке среза данных служба фабрики данных автоматически создает кластер HDInsight **под управлением Linux** .</span><span class="sxs-lookup"><span data-stu-id="40635-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="40635-2711">Дополнительные сведения см. в статье [Вычислительные среды, поддерживаемые фабрикой данных Azure](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="40635-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="40635-2712">Имеющийся кластер Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="40635-2713">Чтобы зарегистрировать собственный кластер HDInsight в фабрике данных, вы можете создать связанную службу Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="40635-2714">В этой связанной службе можно выполнить следующие действия преобразования: [настраиваемое действие .NET](#net-custom-activity), [действие Hive](#hdinsight-hive-activity), [действие Pig] (#hdinsight-pig-activity), [действие MapReduce](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [действие Spark](#hdinsight-spark-activity).</span><span class="sxs-lookup"><span data-stu-id="40635-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2715">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2715">Linked service</span></span>
<span data-ttu-id="40635-2716">Следующая таблица содержит описание свойств, используемых в определении Azure JSON связанной службы Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="40635-2717">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2717">Property</span></span> | <span data-ttu-id="40635-2718">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2718">Description</span></span> | <span data-ttu-id="40635-2719">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2720">type</span><span class="sxs-lookup"><span data-stu-id="40635-2720">type</span></span> |<span data-ttu-id="40635-2721">Свойству type необходимо присвоить значение **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="40635-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="40635-2722">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2722">Yes</span></span> |
| <span data-ttu-id="40635-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="40635-2723">clusterUri</span></span> |<span data-ttu-id="40635-2724">Универсальный код ресурса (URI) кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="40635-2725">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2725">Yes</span></span> |
| <span data-ttu-id="40635-2726">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2726">username</span></span> |<span data-ttu-id="40635-2727">Укажите имя пользователя, которое будет использоваться для подключения к существующему кластеру HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="40635-2728">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2728">Yes</span></span> |
| <span data-ttu-id="40635-2729">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-2729">password</span></span> |<span data-ttu-id="40635-2730">Укажите пароль для учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2730">Specify password for the user account.</span></span> |<span data-ttu-id="40635-2731">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2731">Yes</span></span> |
| <span data-ttu-id="40635-2732">linkedServiceName (имя связанной службы)</span><span class="sxs-lookup"><span data-stu-id="40635-2732">linkedServiceName</span></span> | <span data-ttu-id="40635-2733">Имя связанной службы для службы хранилища Azure, которая обращается к хранилищу BLOB-объектов Azure, используемому кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="40635-2734">В настоящее время для этого свойства невозможно указать связанную службу Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40635-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="40635-2735">Вы можете получать доступ к данным в Azure Data Lake Store из сценариев Hive или Pig, если кластер HDInsight имеет доступ к Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="40635-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="40635-2736">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2736">Yes</span></span> |

<span data-ttu-id="40635-2737">Список поддерживаемых версий кластеров HDInsight см. в статье [Поддерживаемые версии HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span><span class="sxs-lookup"><span data-stu-id="40635-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="40635-2738">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="40635-2739">Пакетная служба Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2739">Azure Batch</span></span>
<span data-ttu-id="40635-2740">Чтобы зарегистрировать пакетный пул виртуальных машин в фабрике данных, можно создать связанную пакетную службу Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="40635-2741">Пользовательские действия .NET можно выполнять с помощью пакетной службы Azure или службы Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="40635-2742">В этой связанной службе можно запустить [настраиваемое действие .NET](#net-custom-activity).</span><span class="sxs-lookup"><span data-stu-id="40635-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2743">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2743">Linked service</span></span>
<span data-ttu-id="40635-2744">Следующая таблица содержит описание свойств, используемых в определении Azure JSON связанной пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="40635-2745">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2745">Property</span></span> | <span data-ttu-id="40635-2746">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2746">Description</span></span> | <span data-ttu-id="40635-2747">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2748">type</span><span class="sxs-lookup"><span data-stu-id="40635-2748">type</span></span> |<span data-ttu-id="40635-2749">Свойству type необходимо присвоить значение **AzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="40635-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="40635-2750">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2750">Yes</span></span> |
| <span data-ttu-id="40635-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="40635-2751">accountName</span></span> |<span data-ttu-id="40635-2752">Имя учетной записи пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="40635-2753">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2753">Yes</span></span> |
| <span data-ttu-id="40635-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="40635-2754">accessKey</span></span> |<span data-ttu-id="40635-2755">Ключ доступа к учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="40635-2756">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2756">Yes</span></span> |
| <span data-ttu-id="40635-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="40635-2757">poolName</span></span> |<span data-ttu-id="40635-2758">Имя пула виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="40635-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="40635-2759">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2759">Yes</span></span> |
| <span data-ttu-id="40635-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="40635-2760">linkedServiceName</span></span> |<span data-ttu-id="40635-2761">Имя связанной службы хранилища Azure, которая ассоциируется с этой связанной пакетной службой Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="40635-2762">Эта связанная служба используется для промежуточных файлов, необходимых для выполнения действий и хранения журналов выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="40635-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="40635-2763">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="40635-2764">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="40635-2765">Машинное обучение Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2765">Azure Machine Learning</span></span>
<span data-ttu-id="40635-2766">Создайте связанную службу Машинного обучения Azure, чтобы зарегистрировать конечную точку пакетной оценки показателей машинного обучения оценки в фабрике данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="40635-2767">В этой связанной службе можно выполнять два действия преобразования данных: [действие выполнения пакета в службе машинного обучения](#machine-learning-batch-execution-activity), [действие обновления ресурса службы машинного обучения](#machine-learning-update-resource-activity).</span><span class="sxs-lookup"><span data-stu-id="40635-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2768">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2768">Linked service</span></span>
<span data-ttu-id="40635-2769">Следующая таблица содержит описание свойств, используемых в определении Azure JSON связанной службы машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="40635-2770">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2770">Property</span></span> | <span data-ttu-id="40635-2771">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2771">Description</span></span> | <span data-ttu-id="40635-2772">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2773">type</span><span class="sxs-lookup"><span data-stu-id="40635-2773">Type</span></span> |<span data-ttu-id="40635-2774">Свойству type необходимо присвоить значение **AzureML**.</span><span class="sxs-lookup"><span data-stu-id="40635-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="40635-2775">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2775">Yes</span></span> |
| <span data-ttu-id="40635-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="40635-2776">mlEndpoint</span></span> |<span data-ttu-id="40635-2777">URL-адрес пакетной оценки.</span><span class="sxs-lookup"><span data-stu-id="40635-2777">The batch scoring URL.</span></span> |<span data-ttu-id="40635-2778">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2778">Yes</span></span> |
| <span data-ttu-id="40635-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="40635-2779">apiKey</span></span> |<span data-ttu-id="40635-2780">API модели опубликованной рабочей области.</span><span class="sxs-lookup"><span data-stu-id="40635-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="40635-2781">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="40635-2782">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="40635-2783">Аналитика озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="40635-2784">Можно создать связанную службу **аналитики озера данных Azure** , чтобы связать службу вычислений аналитики озера данных Azure с фабрикой данных Azure, прежде чем использовать [действие U-SQL аналитики озера данных](data-factory-usql-activity.md) в конвейере.</span><span class="sxs-lookup"><span data-stu-id="40635-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="40635-2785">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2785">Linked service</span></span>

<span data-ttu-id="40635-2786">Следующая таблица содержит описание свойств, используемых в определении JSON связанной службы Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="40635-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="40635-2787">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2787">Property</span></span> | <span data-ttu-id="40635-2788">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2788">Description</span></span> | <span data-ttu-id="40635-2789">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2790">Тип</span><span class="sxs-lookup"><span data-stu-id="40635-2790">Type</span></span> |<span data-ttu-id="40635-2791">Свойству type необходимо присвоить значение **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="40635-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="40635-2792">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2792">Yes</span></span> |
| <span data-ttu-id="40635-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="40635-2793">accountName</span></span> |<span data-ttu-id="40635-2794">Имя учетной записи аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="40635-2795">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2795">Yes</span></span> |
| <span data-ttu-id="40635-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="40635-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="40635-2797">Универсальный код ресурса (URI) аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="40635-2798">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2798">No</span></span> |
| <span data-ttu-id="40635-2799">authorization</span><span class="sxs-lookup"><span data-stu-id="40635-2799">authorization</span></span> |<span data-ttu-id="40635-2800">Код авторизации извлекается автоматически после нажатия кнопки **Авторизовать** в редакторе фабрики данных и выполнения входа с авторизацией OAuth.</span><span class="sxs-lookup"><span data-stu-id="40635-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="40635-2801">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2801">Yes</span></span> |
| <span data-ttu-id="40635-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="40635-2802">subscriptionId</span></span> |<span data-ttu-id="40635-2803">Идентификатор подписки Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2803">Azure subscription id</span></span> |<span data-ttu-id="40635-2804">Нет (если не указан, используется подписка фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="40635-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="40635-2805">имя_группы_ресурсов</span><span class="sxs-lookup"><span data-stu-id="40635-2805">resourceGroupName</span></span> |<span data-ttu-id="40635-2806">Имя группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2806">Azure resource group name</span></span> |<span data-ttu-id="40635-2807">Нет (если не указано, используется группа ресурсов фабрики данных).</span><span class="sxs-lookup"><span data-stu-id="40635-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="40635-2808">sessionid</span><span class="sxs-lookup"><span data-stu-id="40635-2808">sessionId</span></span> |<span data-ttu-id="40635-2809">Идентификатор сеанса из сеанса авторизации OAuth.</span><span class="sxs-lookup"><span data-stu-id="40635-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="40635-2810">Каждый идентификатор сеанса является уникальным и используется только один раз.</span><span class="sxs-lookup"><span data-stu-id="40635-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="40635-2811">При использовании редактора фабрики данных этот идентификатор создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="40635-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="40635-2812">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="40635-2813">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2813">JSON example</span></span>
<span data-ttu-id="40635-2814">В следующем примере представлено определение JSON для связанной службы аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="40635-2815">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2815">Azure SQL Database</span></span>
<span data-ttu-id="40635-2816">Связанная служба SQL Azure создается и применяется к [действию хранимой процедуры](#stored-procedure-activity) для вызова хранимой процедуры из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2817">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2817">Linked service</span></span>
<span data-ttu-id="40635-2818">Для определения связанной службы базы данных SQL Azure задайте **AzureSqlDatabase** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2819">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2819">Property</span></span> | <span data-ttu-id="40635-2820">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2820">Description</span></span> | <span data-ttu-id="40635-2821">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-2822">connectionString</span></span> |<span data-ttu-id="40635-2823">В свойстве connectionString указываются сведения, необходимые для подключения к экземпляру базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="40635-2824">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="40635-2825">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2825">JSON example</span></span>

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

<span data-ttu-id="40635-2826">Дополнительную информацию см. в статье о [связанной службе SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="40635-2827">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="40635-2828">Связанная служба хранилища данных SQL Azure создается и применяется к [действию хранимой процедуры](data-factory-stored-proc-activity.md) для вызова хранимой процедуры из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2829">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2829">Linked service</span></span>
<span data-ttu-id="40635-2830">Для определения связанной службы хранилища данных SQL Azure задайте **AzureSqlDW** в качестве **типа** связанной службы и укажите в разделе **typeProperties** следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="40635-2831">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2831">Property</span></span> | <span data-ttu-id="40635-2832">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2832">Description</span></span> | <span data-ttu-id="40635-2833">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-2834">connectionString</span></span> |<span data-ttu-id="40635-2835">Укажите сведения, необходимые для подключения к экземпляру хранилища данных SQL Azure, для свойства connectionString.</span><span class="sxs-lookup"><span data-stu-id="40635-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="40635-2836">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="40635-2837">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2837">JSON example</span></span>

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

<span data-ttu-id="40635-2838">Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="40635-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40635-2839">SQL Server</span></span> 
<span data-ttu-id="40635-2840">Связанная служба SQL Server создается и применяется к [действию хранимой процедуры](data-factory-stored-proc-activity.md) для вызова хранимой процедуры из конвейера фабрики данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="40635-2841">Связанные службы</span><span class="sxs-lookup"><span data-stu-id="40635-2841">Linked service</span></span>
<span data-ttu-id="40635-2842">Создайте связанную службу типа **OnPremisesSqlServer**, чтобы связать локальную базу данных SQL Server с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="40635-2843">В следующей таблице содержится описание элементов JSON, которые относятся к локальной связанной службе SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="40635-2844">В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="40635-2845">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2845">Property</span></span> | <span data-ttu-id="40635-2846">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2846">Description</span></span> | <span data-ttu-id="40635-2847">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2848">type</span><span class="sxs-lookup"><span data-stu-id="40635-2848">type</span></span> |<span data-ttu-id="40635-2849">Свойству type необходимо присвоить значение **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="40635-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="40635-2850">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2850">Yes</span></span> |
| <span data-ttu-id="40635-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="40635-2851">connectionString</span></span> |<span data-ttu-id="40635-2852">Укажите сведения о параметре connectionString, необходимые для подключения к локальной базе данных SQL Server с помощью проверки подлинности SQL или проверки подлинности Windows.</span><span class="sxs-lookup"><span data-stu-id="40635-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="40635-2853">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2853">Yes</span></span> |
| <span data-ttu-id="40635-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="40635-2854">gatewayName</span></span> |<span data-ttu-id="40635-2855">Имя шлюза, который службе фабрики данных следует использовать для подключения к локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="40635-2856">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2856">Yes</span></span> |
| <span data-ttu-id="40635-2857">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="40635-2857">username</span></span> |<span data-ttu-id="40635-2858">При использовании проверки подлинности Windows укажите имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="40635-2859">Например, **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="40635-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="40635-2860">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2860">No</span></span> |
| <span data-ttu-id="40635-2861">пароль</span><span class="sxs-lookup"><span data-stu-id="40635-2861">password</span></span> |<span data-ttu-id="40635-2862">Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="40635-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="40635-2863">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2863">No</span></span> |

<span data-ttu-id="40635-2864">Вы можете зашифровать учетные данные с помощью командлета **New-AzureRmDataFactoryEncryptValue** и использовать их в строке подключения, как показано в следующем примере (свойство **EncryptedCredential**):</span><span class="sxs-lookup"><span data-stu-id="40635-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="40635-2865">Пример: JSON для использования проверки подлинности SQL</span><span class="sxs-lookup"><span data-stu-id="40635-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="40635-2866">Пример: JSON для использования проверки подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="40635-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="40635-2867">Если указаны имя пользователя и пароль, то шлюз использует их, чтобы действовать от имени соответствующей учетной записи пользователя для подключения к локальной базе данных SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40635-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="40635-2868">В противном случае шлюз подключается к SQL Server напрямую с помощью контекста безопасности шлюза (его стартовая учетная запись).</span><span class="sxs-lookup"><span data-stu-id="40635-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="40635-2869">Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="40635-2870">Действия преобразования данных</span><span class="sxs-lookup"><span data-stu-id="40635-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="40635-2871">Действие</span><span class="sxs-lookup"><span data-stu-id="40635-2871">Activity</span></span> | <span data-ttu-id="40635-2872">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="40635-2873">Действие Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="40635-2874">Действие Hive HDInsight в конвейере фабрики данных выполняет запросы Hive к вашему собственному кластеру HDInsight или кластеру HDInsight по запросу под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="40635-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="40635-2875">Действие Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="40635-2876">Действие Pig HDInsight в конвейере фабрики данных выполняет запросы Pig к вашему собственному кластеру HDInsight или кластеру HDInsight по запросу под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="40635-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="40635-2877">Действие MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="40635-2878">Действие MapReduce HDInsight в конвейере фабрики данных выполняет программы MapReduce для вашего собственного кластера HDInsight или кластера HDInsight по запросу под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="40635-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="40635-2879">Действие потоковой передачи HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="40635-2880">Действие потоковой передачи HDInsight в конвейере фабрики данных выполняет программы потоковой передачи Hadoop для вашего собственного кластера HDInsight или кластера HDInsight по запросу под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="40635-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="40635-2881">Действие HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="40635-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="40635-2882">Действие HDInsight Spark в конвейере фабрики данных выполняет программы Spark в вашем кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="40635-2883">Действие выполнения пакета машинного обучения</span><span class="sxs-lookup"><span data-stu-id="40635-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="40635-2884">Фабрика данных Azure позволяет легко создавать конвейеры, в которых для прогнозной аналитики используется опубликованная веб-служба Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="40635-2885">С помощью действия выполнения пакета в конвейере фабрики данных Azure можно вызывать веб-службу Машинного обучения Azure, чтобы создавать прогнозы по данным в пакете.</span><span class="sxs-lookup"><span data-stu-id="40635-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="40635-2886">Действие "Обновить ресурс" в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="40635-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="40635-2887">Со временем прогнозные модели в оценивающих экспериментах машинного обучения потребуют повторного обучения с помощью новых входных наборов данных.</span><span class="sxs-lookup"><span data-stu-id="40635-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="40635-2888">Когда повторное обучение будет завершено, вам потребуется обновить веб-службу оценки на основании обновленной модели машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="40635-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="40635-2889">Чтобы обновить веб-службу с помощью заново обученной модели, можно использовать действие обновления ресурса Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="40635-2890">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="40635-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="40635-2891">C помощью действия хранимой процедуры в конвейере фабрики данных можно вызвать хранимую процедуру из одного из следующих хранилищ данных: база данных SQL Azure, хранилище данных SQL Azure, база данных SQL Server вашего предприятия или виртуальная машина Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="40635-2892">Действие U-SQL в Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="40635-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="40635-2893">Действие U-SQL Data Lake Analytics запускает сценарий U-SQL для кластера Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="40635-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="40635-2894">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="40635-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="40635-2895">Если вам нужно преобразовать данные способом, который не поддерживается фабрикой данных Azure, то можно создать настраиваемое действие с собственной логикой обработки данных и использовать это действие в конвейере.</span><span class="sxs-lookup"><span data-stu-id="40635-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="40635-2896">Можно настроить запуск настраиваемого действия .NET с помощью пакетной службы Azure или кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="40635-2897">Действие Hive HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="40635-2898">В определении JSON действия Hive можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="40635-2899">Свойству type присваивается значение **HDInsightHive**.</span><span class="sxs-lookup"><span data-stu-id="40635-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="40635-2900">Сначала нужно создать связанную службу HDInsight и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-2901">В разделе **typeProperties** при установке HDInsightHive в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="40635-2902">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2902">Property</span></span> | <span data-ttu-id="40635-2903">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2903">Description</span></span> | <span data-ttu-id="40635-2904">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2905">script</span><span class="sxs-lookup"><span data-stu-id="40635-2905">script</span></span> |<span data-ttu-id="40635-2906">Указывается встроенный сценарий Hive.</span><span class="sxs-lookup"><span data-stu-id="40635-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="40635-2907">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2907">No</span></span> |
| <span data-ttu-id="40635-2908">script path</span><span class="sxs-lookup"><span data-stu-id="40635-2908">script path</span></span> |<span data-ttu-id="40635-2909">Путь к файлу сценария Hive в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="40635-2910">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="40635-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="40635-2911">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="40635-2911">Both cannot be used together.</span></span> <span data-ttu-id="40635-2912">В имени файла учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="40635-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="40635-2913">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2913">No</span></span> |
| <span data-ttu-id="40635-2914">defines</span><span class="sxs-lookup"><span data-stu-id="40635-2914">defines</span></span> |<span data-ttu-id="40635-2915">Параметры в виде пары "ключ-значение", ссылки на которые указываются в сценарии Hive с помощью элемента hiveconf.</span><span class="sxs-lookup"><span data-stu-id="40635-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="40635-2916">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2916">No</span></span> |

<span data-ttu-id="40635-2917">Эти свойства type относятся к действию Hive.</span><span class="sxs-lookup"><span data-stu-id="40635-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="40635-2918">Другие свойства (за пределами раздела typeProperties) поддерживаются для всех действий.</span><span class="sxs-lookup"><span data-stu-id="40635-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="40635-2919">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2919">JSON example</span></span>
<span data-ttu-id="40635-2920">Ниже приведен фрагмент JSON, определяющий действие HDInsight Hive в конвейере.</span><span class="sxs-lookup"><span data-stu-id="40635-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="40635-2921">Дополнительные сведения см. в статье о [действии Hive](data-factory-hive-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40635-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="40635-2922">Действие Pig HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="40635-2923">В определении JSON действия Pig можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="40635-2924">Свойству type присваивается значение **HDInsightPig**.</span><span class="sxs-lookup"><span data-stu-id="40635-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="40635-2925">Сначала нужно создать связанную службу HDInsight и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-2926">В разделе **typeProperties** при установке HDInsightPig в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="40635-2927">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2927">Property</span></span> | <span data-ttu-id="40635-2928">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2928">Description</span></span> | <span data-ttu-id="40635-2929">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2930">script</span><span class="sxs-lookup"><span data-stu-id="40635-2930">script</span></span> |<span data-ttu-id="40635-2931">Указывается встроенный сценарий Pig.</span><span class="sxs-lookup"><span data-stu-id="40635-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="40635-2932">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2932">No</span></span> |
| <span data-ttu-id="40635-2933">script path</span><span class="sxs-lookup"><span data-stu-id="40635-2933">script path</span></span> |<span data-ttu-id="40635-2934">Путь к файлу сценария Pig в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="40635-2935">Можно использовать либо свойство script, либо свойство scriptPath,</span><span class="sxs-lookup"><span data-stu-id="40635-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="40635-2936">но не оба сразу.</span><span class="sxs-lookup"><span data-stu-id="40635-2936">Both cannot be used together.</span></span> <span data-ttu-id="40635-2937">В имени файла учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="40635-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="40635-2938">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2938">No</span></span> |
| <span data-ttu-id="40635-2939">defines</span><span class="sxs-lookup"><span data-stu-id="40635-2939">defines</span></span> |<span data-ttu-id="40635-2940">Параметры в виде пары "ключ — значение", ссылки на которые указываются в сценарии Pig.</span><span class="sxs-lookup"><span data-stu-id="40635-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="40635-2941">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2941">No</span></span> |

<span data-ttu-id="40635-2942">Эти свойства type относятся к действию Pig.</span><span class="sxs-lookup"><span data-stu-id="40635-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="40635-2943">Другие свойства (за пределами раздела typeProperties) поддерживаются для всех действий.</span><span class="sxs-lookup"><span data-stu-id="40635-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="40635-2944">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2944">JSON example</span></span>

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

<span data-ttu-id="40635-2945">Дополнительные сведения см. в статье о [действии Pig](#data-factory-pig-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40635-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="40635-2946">Действие MapReduce HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="40635-2947">В определении JSON действия MapReduce можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="40635-2948">Свойству type присваивается значение **HDInsightMapReduce**.</span><span class="sxs-lookup"><span data-stu-id="40635-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="40635-2949">Сначала нужно создать связанную службу HDInsight и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-2950">В разделе **typeProperties** при установке HDInsightMapReduce в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="40635-2951">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2951">Property</span></span> | <span data-ttu-id="40635-2952">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2952">Description</span></span> | <span data-ttu-id="40635-2953">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="40635-2954">jarLinkedService</span></span> | <span data-ttu-id="40635-2955">Имя связанной службы для службы хранилища Azure, содержащей JAR-файл.</span><span class="sxs-lookup"><span data-stu-id="40635-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="40635-2956">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2956">Yes</span></span> |
| <span data-ttu-id="40635-2957">jarFilePath</span><span class="sxs-lookup"><span data-stu-id="40635-2957">jarFilePath</span></span> | <span data-ttu-id="40635-2958">Путь к JAR-файлу в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="40635-2959">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2959">Yes</span></span> | 
| <span data-ttu-id="40635-2960">className</span><span class="sxs-lookup"><span data-stu-id="40635-2960">className</span></span> | <span data-ttu-id="40635-2961">Имя основного класса в JAR-файле.</span><span class="sxs-lookup"><span data-stu-id="40635-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="40635-2962">Да</span><span class="sxs-lookup"><span data-stu-id="40635-2962">Yes</span></span> | 
| <span data-ttu-id="40635-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="40635-2963">arguments</span></span> | <span data-ttu-id="40635-2964">Список разделенных запятыми аргументов для программы MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40635-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="40635-2965">Во время выполнения вы увидите несколько дополнительных аргументов (например, mapreduce.job.tags) платформы MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40635-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="40635-2966">Чтобы отличать свои аргументы от аргументов MapReduce, вы можете использовать параметр и значение в качестве аргументов, как показано в следующем примере (-s, --input, --output и т. д. — параметры, за которыми сразу следуют их значения).</span><span class="sxs-lookup"><span data-stu-id="40635-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="40635-2967">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40635-2968">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
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
                "description": "Custom Map Reduce to generate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="40635-2969">Дополнительные сведения см. в статье о [действии MapReduce](data-factory-map-reduce.md).</span><span class="sxs-lookup"><span data-stu-id="40635-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="40635-2970">Действие потоковой передачи HDInsight</span><span class="sxs-lookup"><span data-stu-id="40635-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="40635-2971">В определении JSON действия потоковой передачи Hadoop можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="40635-2972">Свойству type присваивается значение **HDInsightStreaming**.</span><span class="sxs-lookup"><span data-stu-id="40635-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="40635-2973">Сначала нужно создать связанную службу HDInsight и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-2974">В разделе **typeProperties** при установке HDInsightStreaming в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="40635-2975">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-2975">Property</span></span> | <span data-ttu-id="40635-2976">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="40635-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="40635-2977">mapper</span></span> | <span data-ttu-id="40635-2978">Имя исполняемого файла средства сопоставления.</span><span class="sxs-lookup"><span data-stu-id="40635-2978">Name of the mapper executable.</span></span> <span data-ttu-id="40635-2979">В этом примере таким файлом является cat.exe.</span><span class="sxs-lookup"><span data-stu-id="40635-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="40635-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="40635-2980">reducer</span></span> | <span data-ttu-id="40635-2981">Имя исполняемого файла средства приведения.</span><span class="sxs-lookup"><span data-stu-id="40635-2981">Name of the reducer executable.</span></span> <span data-ttu-id="40635-2982">В этом примере таким файлом является wc.exe.</span><span class="sxs-lookup"><span data-stu-id="40635-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="40635-2983">input</span><span class="sxs-lookup"><span data-stu-id="40635-2983">input</span></span> | <span data-ttu-id="40635-2984">Входной файл (включая расположение) для средства сопоставления.</span><span class="sxs-lookup"><span data-stu-id="40635-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="40635-2985">В примере "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt" adfsample — это контейнер BLOB-объектов, example/data/Gutenberg — это папка, а davinci.txt — это двоичный большой объект.</span><span class="sxs-lookup"><span data-stu-id="40635-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="40635-2986">output</span><span class="sxs-lookup"><span data-stu-id="40635-2986">output</span></span> | <span data-ttu-id="40635-2987">Выходной файл (включая расположение) для средства приведения.</span><span class="sxs-lookup"><span data-stu-id="40635-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="40635-2988">Результат задания потоковой передачи Hadoop записывается в расположение, заданное для этого свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="40635-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="40635-2989">filePaths</span></span> | <span data-ttu-id="40635-2990">Пути к исполняемым файлам средства сопоставления и приведения.</span><span class="sxs-lookup"><span data-stu-id="40635-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="40635-2991">В примере adfsample/example/apps/wc.exe adfsample — это контейнер больших двоичных объектов, example/apps — это папка, а wc.exe — это исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="40635-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="40635-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="40635-2992">fileLinkedService</span></span> | <span data-ttu-id="40635-2993">Связанная служба хранилища Azure, представляющая хранилище Azure, где хранятся указанные в разделе filePaths файлы.</span><span class="sxs-lookup"><span data-stu-id="40635-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="40635-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="40635-2994">arguments</span></span> | <span data-ttu-id="40635-2995">Список разделенных запятыми аргументов для программы MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40635-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="40635-2996">Во время выполнения вы увидите несколько дополнительных аргументов (например, mapreduce.job.tags) платформы MapReduce.</span><span class="sxs-lookup"><span data-stu-id="40635-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="40635-2997">Чтобы отличать свои аргументы от аргументов MapReduce, вы можете использовать параметр и значение в качестве аргументов, как показано в следующем примере (-s, --input, --output и т. д. — параметры, за которыми сразу следуют их значения).</span><span class="sxs-lookup"><span data-stu-id="40635-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="40635-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="40635-2998">getDebugInfo</span></span> | <span data-ttu-id="40635-2999">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="40635-2999">An optional element.</span></span> <span data-ttu-id="40635-3000">Если для него установлено значение Failure, журналы скачиваются только при сбое.</span><span class="sxs-lookup"><span data-stu-id="40635-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="40635-3001">Если для него установлено значение All, журналы скачиваются всегда, независимо от состояния выполнения.</span><span class="sxs-lookup"><span data-stu-id="40635-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="40635-3002">Вам нужно указать выходной набор данных для действия потоковой передачи Hadoop для свойства **outputs**.</span><span class="sxs-lookup"><span data-stu-id="40635-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="40635-3003">Это может быть просто фиктивный набор данных, необходимый для соблюдения расписания конвейера (ежечасно, ежедневно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="40635-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="40635-3004">Если действие не принимает входные данные, можно не указывать входной набор данных для действия для свойства **inputs**.</span><span class="sxs-lookup"><span data-stu-id="40635-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="40635-3005">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3005">JSON example</span></span>

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

<span data-ttu-id="40635-3006">Дополнительные сведения см. в статье о [действии потоковой передачи Hadoop](data-factory-hadoop-streaming-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40635-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="40635-3007">Действие HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="40635-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="40635-3008">В определении JSON действия Spark можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="40635-3009">Свойству type присваивается значение **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="40635-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="40635-3010">Сначала нужно создать связанную службу HDInsight и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-3011">В разделе **typeProperties** при установке HDInsightSpark в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="40635-3012">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-3012">Property</span></span> | <span data-ttu-id="40635-3013">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-3013">Description</span></span> | <span data-ttu-id="40635-3014">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="40635-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="40635-3015">rootPath</span></span> | <span data-ttu-id="40635-3016">Контейнер BLOB-объектов Azure и папка, содержащая файл Spark.</span><span class="sxs-lookup"><span data-stu-id="40635-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="40635-3017">В имени файла учитывается регистр знаков.</span><span class="sxs-lookup"><span data-stu-id="40635-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="40635-3018">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3018">Yes</span></span> |
| <span data-ttu-id="40635-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="40635-3019">entryFilePath</span></span> | <span data-ttu-id="40635-3020">Относительный путь к корневой папке пакета и кода Spark.</span><span class="sxs-lookup"><span data-stu-id="40635-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="40635-3021">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3021">Yes</span></span> |
| <span data-ttu-id="40635-3022">className</span><span class="sxs-lookup"><span data-stu-id="40635-3022">className</span></span> | <span data-ttu-id="40635-3023">Основной класс Java или Spark приложения.</span><span class="sxs-lookup"><span data-stu-id="40635-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="40635-3024">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3024">No</span></span> | 
| <span data-ttu-id="40635-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="40635-3025">arguments</span></span> | <span data-ttu-id="40635-3026">Список аргументов командной строки для программы Spark.</span><span class="sxs-lookup"><span data-stu-id="40635-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="40635-3027">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3027">No</span></span> | 
| <span data-ttu-id="40635-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="40635-3028">proxyUser</span></span> | <span data-ttu-id="40635-3029">Учетная запись пользователя для олицетворения, используемая для выполнения программы Spark.</span><span class="sxs-lookup"><span data-stu-id="40635-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="40635-3030">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3030">No</span></span> | 
| <span data-ttu-id="40635-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="40635-3031">sparkConfig</span></span> | <span data-ttu-id="40635-3032">Свойства конфигурации Spark.</span><span class="sxs-lookup"><span data-stu-id="40635-3032">Spark configuration properties.</span></span> | <span data-ttu-id="40635-3033">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3033">No</span></span> | 
| <span data-ttu-id="40635-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="40635-3034">getDebugInfo</span></span> | <span data-ttu-id="40635-3035">Указывает, когда файлы журнала Spark копируются в службу хранилища Azure, используемое кластером HDInsight или определенное sparkJobLinkedService.</span><span class="sxs-lookup"><span data-stu-id="40635-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="40635-3036">Допустимые значения: None, Always или Failure.</span><span class="sxs-lookup"><span data-stu-id="40635-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="40635-3037">Значение по умолчанию: None.</span><span class="sxs-lookup"><span data-stu-id="40635-3037">Default value: None.</span></span> | <span data-ttu-id="40635-3038">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3038">No</span></span> | 
| <span data-ttu-id="40635-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="40635-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="40635-3040">Связанная служба службы хранилища Azure, в которой хранятся файл задания Spark, зависимости и журналы.</span><span class="sxs-lookup"><span data-stu-id="40635-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="40635-3041">Если значение этого свойства не указано, используется хранилище, связанное с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="40635-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="40635-3042">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="40635-3043">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3043">JSON example</span></span>

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
<span data-ttu-id="40635-3044">Обратите внимание на следующие моменты.</span><span class="sxs-lookup"><span data-stu-id="40635-3044">Note the following points:</span></span> 

- <span data-ttu-id="40635-3045">Свойству **type** присваивается значение **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="40635-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="40635-3046">Свойству **rootPath** присваивается значение **adfspark\\pyFiles**, где adfspark — контейнер больших двоичных объектов Azure, а pyFiles — папка с файлами в этом контейнере.</span><span class="sxs-lookup"><span data-stu-id="40635-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="40635-3047">В этом примере хранилище BLOB-объектов Azure связано с кластером Spark.</span><span class="sxs-lookup"><span data-stu-id="40635-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="40635-3048">Файл можно отправить в другое хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="40635-3049">Чтобы сделать это, создайте связанную службу хранилища Azure, которая свяжет эту учетную запись хранения с фабрикой данных.</span><span class="sxs-lookup"><span data-stu-id="40635-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="40635-3050">Затем укажите имя связанной службы в качестве значения свойства **sparkJobLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="40635-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="40635-3051">Сведения об этом свойстве и других свойствах, поддерживаемых действием Spark, см. в [этом разделе](#spark-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="40635-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="40635-3052">Свойству **entryFilePath** присваивается значение **test.py**, которое является файлом Python.</span><span class="sxs-lookup"><span data-stu-id="40635-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="40635-3053">Свойству **getDebugInfo** присваивается значение **Always**. Так файлы журналов будут создаваться постоянно (успешные и неудачные события).</span><span class="sxs-lookup"><span data-stu-id="40635-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="40635-3054">Если вы не устраняете неполадки, мы советуем не устанавливать для этого свойства значение Always в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="40635-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="40635-3055">В разделе **outputs** содержится один выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="40635-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="40635-3056">Вы должны определить выходной набор данных, даже если программа Spark не выдает выходные данные.</span><span class="sxs-lookup"><span data-stu-id="40635-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="40635-3057">На основе этого набора настраивается расписание конвейера (ежечасно, ежедневно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="40635-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="40635-3058">Дополнительные сведения о действии Spark см. в [этой статье](data-factory-spark.md).</span><span class="sxs-lookup"><span data-stu-id="40635-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="40635-3059">Действие выполнения пакета в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="40635-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="40635-3060">В определении JSON действия выполнения пакета в Машинном обучении Azure можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="40635-3061">Свойству type действия присваивается значение **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="40635-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="40635-3062">Сначала нужно создать связанную службу машинного обучения Azure и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-3063">В разделе **typeProperties** при установке AzureMLBatchExecution в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="40635-3064">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-3064">Property</span></span> | <span data-ttu-id="40635-3065">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-3065">Description</span></span> | <span data-ttu-id="40635-3066">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="40635-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="40635-3067">webServiceInput</span></span> | <span data-ttu-id="40635-3068">Набор данных, передаваемый в качестве входных данных для веб-службы Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="40635-3069">Его также следует включить в качестве входных данных для действия.</span><span class="sxs-lookup"><span data-stu-id="40635-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="40635-3070">Используйте webServiceInput или webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="40635-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="40635-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="40635-3071">webServiceInputs</span></span> | <span data-ttu-id="40635-3072">Укажите наборы данных, передаваемый в качестве входных данных для веб-службы Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="40635-3073">Если веб-служба принимает несколько входных наборов данных, используйте свойство webServiceInputs вместо webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="40635-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="40635-3074">Наборы данных, на которые ссылается свойство **webServiceInputs**, также должны быть включены в раздел **inputs** действия.</span><span class="sxs-lookup"><span data-stu-id="40635-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="40635-3075">Используйте webServiceInput или webServiceInputs.</span><span class="sxs-lookup"><span data-stu-id="40635-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="40635-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="40635-3076">webServiceOutputs</span></span> | <span data-ttu-id="40635-3077">Наборы данных, присваиваемые в качестве выходных данных для веб-службы Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="40635-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="40635-3078">Веб-служба возвращает выходные данные в этом наборе данных.</span><span class="sxs-lookup"><span data-stu-id="40635-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="40635-3079">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3079">Yes</span></span> | 
<span data-ttu-id="40635-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="40635-3080">globalParameters</span></span> | <span data-ttu-id="40635-3081">Укажите значения параметров веб-службы в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="40635-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="40635-3082">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40635-3083">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3083">JSON example</span></span>
<span data-ttu-id="40635-3084">В этом примере у действия имеется входной (**MLSqlInput**) и выходной наборы данных (**MLSqlOutput**).</span><span class="sxs-lookup"><span data-stu-id="40635-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="40635-3085">Набор **MLSqlInput** передается в веб-службу в качестве входных данных с помощью свойства JSON **webServiceInput**,</span><span class="sxs-lookup"><span data-stu-id="40635-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="40635-3086">а **MLSqlOutput** — в качестве выходных данных с помощью свойства JSON **webServiceOutputs**.</span><span class="sxs-lookup"><span data-stu-id="40635-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="40635-3087">В примере JSON развернутая веб-служба Машинного обучения Azure использует модуль чтения и модуль записи для чтения данных из базы данных SQL Azure и записи их в нее.</span><span class="sxs-lookup"><span data-stu-id="40635-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="40635-3088">Эта веб-служба предоставляет следующие параметры: Database server name, Database name, Server user account name и Server user account password.</span><span class="sxs-lookup"><span data-stu-id="40635-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="40635-3089">Только входные и выходные данные действия AzureMLBatchExecution могут передаваться как параметры веб-службы.</span><span class="sxs-lookup"><span data-stu-id="40635-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="40635-3090">Например, в приведенном выше фрагменте JSON MLSqlInput —входные данные действия AzureMLBatchExecution, передаваемые в качестве входных данных в веб-службу через параметр webServiceInput.</span><span class="sxs-lookup"><span data-stu-id="40635-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="40635-3091">Действие обновления ресурса в службе машинного обучения</span><span class="sxs-lookup"><span data-stu-id="40635-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="40635-3092">В определении JSON действия обновления ресурса в Машинном обучении Azure можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="40635-3093">Свойству type действия присваивается значение **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="40635-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="40635-3094">Сначала нужно создать связанную службу машинного обучения Azure и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-3095">В разделе **typeProperties** при установке AzureMLUpdateResource в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="40635-3096">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-3096">Property</span></span> | <span data-ttu-id="40635-3097">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-3097">Description</span></span> | <span data-ttu-id="40635-3098">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="40635-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="40635-3099">trainedModelName</span></span> | <span data-ttu-id="40635-3100">Имя переобученной модели.</span><span class="sxs-lookup"><span data-stu-id="40635-3100">Name of the retrained model.</span></span> | <span data-ttu-id="40635-3101">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3101">Yes</span></span> |  
<span data-ttu-id="40635-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="40635-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="40635-3103">Набор данных, указывающий на файл iLearner, возвращенный операцией повторного обучения.</span><span class="sxs-lookup"><span data-stu-id="40635-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="40635-3104">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40635-3105">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3105">JSON example</span></span>
<span data-ttu-id="40635-3106">Конвейер содержит два действия: **AzureMLBatchExecution** и **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="40635-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="40635-3107">Действие "Выполнение пакета" машинного обучения Azure принимает входные данные для обучения и создает выходной файл iLearner.</span><span class="sxs-lookup"><span data-stu-id="40635-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="40635-3108">Это действие обращается к веб-службе обучения (обучающему эксперименту, опубликованному в виде веб-службы), передает ей данные для обучения и получает файл ilearner.</span><span class="sxs-lookup"><span data-stu-id="40635-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="40635-3109">Набор данных placeholderBlob является фиктивным набором данных, который необходим фабрике данных Azure для запуска конвейера.</span><span class="sxs-lookup"><span data-stu-id="40635-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="40635-3110">Действие U-SQL в аналитике озера данных</span><span class="sxs-lookup"><span data-stu-id="40635-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="40635-3111">В определении JSON действия U-SQL можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="40635-3112">Свойству type действия присваивается значение **DataLakeAnalyticsU-SQL**.</span><span class="sxs-lookup"><span data-stu-id="40635-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="40635-3113">Вам нужно создать связанную службу Azure Data Lake Analytics и указать ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-3114">В разделе **typeProperties** при установке DataLakeAnalyticsU-SQL в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="40635-3115">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-3115">Property</span></span> | <span data-ttu-id="40635-3116">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-3116">Description</span></span> | <span data-ttu-id="40635-3117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="40635-3118">scriptPath</span></span> |<span data-ttu-id="40635-3119">Путь к папке, содержащей скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="40635-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="40635-3120">В имени файла учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="40635-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="40635-3121">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="40635-3121">No (if you use script)</span></span> |
| <span data-ttu-id="40635-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="40635-3122">scriptLinkedService</span></span> |<span data-ttu-id="40635-3123">Связанная служба, которая связывает хранилище, содержащее скрипт, с фабрикой данных</span><span class="sxs-lookup"><span data-stu-id="40635-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="40635-3124">Нет (если используется скрипт)</span><span class="sxs-lookup"><span data-stu-id="40635-3124">No (if you use script)</span></span> |
| <span data-ttu-id="40635-3125">script</span><span class="sxs-lookup"><span data-stu-id="40635-3125">script</span></span> |<span data-ttu-id="40635-3126">Указание сценария непосредственно в строке вместо использования scriptPath и scriptLinkedService.</span><span class="sxs-lookup"><span data-stu-id="40635-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="40635-3127">Например: "script" : "CREATE DATABASE test".</span><span class="sxs-lookup"><span data-stu-id="40635-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="40635-3128">Нет (при использовании scriptPath и scriptLinkedService)</span><span class="sxs-lookup"><span data-stu-id="40635-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="40635-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="40635-3129">degreeOfParallelism</span></span> |<span data-ttu-id="40635-3130">Максимальное количество узлов, используемых одновременно для выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="40635-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="40635-3131">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3131">No</span></span> |
| <span data-ttu-id="40635-3132">priority</span><span class="sxs-lookup"><span data-stu-id="40635-3132">priority</span></span> |<span data-ttu-id="40635-3133">Определяет, какие задания из всех в очереди должны запускаться в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="40635-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="40635-3134">Чем меньше число, тем выше приоритет.</span><span class="sxs-lookup"><span data-stu-id="40635-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="40635-3135">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3135">No</span></span> |
| <span data-ttu-id="40635-3136">parameters</span><span class="sxs-lookup"><span data-stu-id="40635-3136">parameters</span></span> |<span data-ttu-id="40635-3137">Параметры скрипта U-SQL</span><span class="sxs-lookup"><span data-stu-id="40635-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="40635-3138">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="40635-3139">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3139">JSON example</span></span>

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

<span data-ttu-id="40635-3140">Дополнительные сведения см. в статье о [действии U-SQL Data Lake Analytics](data-factory-usql-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40635-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="40635-3141">Действие хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="40635-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="40635-3142">В определении JSON действия хранимой процедуры можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="40635-3143">Свойству type действия присваивается значение **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="40635-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="40635-3144">Создайте одну из следующих связанных служб и укажите ее имя в качестве значения свойства **linkedServiceName**:</span><span class="sxs-lookup"><span data-stu-id="40635-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="40635-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="40635-3145">SQL Server</span></span> 
- <span data-ttu-id="40635-3146">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-3146">Azure SQL Database</span></span>
- <span data-ttu-id="40635-3147">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="40635-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="40635-3148">В разделе **typeProperties** при установке SqlServerStoredProcedure в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="40635-3149">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-3149">Property</span></span> | <span data-ttu-id="40635-3150">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-3150">Description</span></span> | <span data-ttu-id="40635-3151">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40635-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="40635-3152">storedProcedureName</span></span> |<span data-ttu-id="40635-3153">Укажите имя хранимой процедуры в базе данных SQL Azure или хранилище данных SQL Azure, представленной связанной службой, которую использует выходная таблица.</span><span class="sxs-lookup"><span data-stu-id="40635-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="40635-3154">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3154">Yes</span></span> |
| <span data-ttu-id="40635-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="40635-3155">storedProcedureParameters</span></span> |<span data-ttu-id="40635-3156">Указываемые значения для параметров хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="40635-3157">Если для параметра необходимо передать значение null, используйте синтаксис param1: null (все символы в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="40635-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="40635-3158">Чтобы научиться использовать это свойство, см. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="40635-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="40635-3159">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3159">No</span></span> |

<span data-ttu-id="40635-3160">При указании входного набора данных он должен быть доступен (в состоянии "Готово") для выполнения действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="40635-3161">Входной набор данных не может потребляться в хранимой процедуре в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="40635-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="40635-3162">Он используется только для проверки зависимости перед запуском действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="40635-3163">Для действия хранимой процедуры необходимо указать выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="40635-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="40635-3164">Выходной набор данных указывает **расписание** для действия хранимой процедуры (ежечасно, еженедельно, ежемесячно и т. д.).</span><span class="sxs-lookup"><span data-stu-id="40635-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="40635-3165">Выходной набор данных должен использовать **связанную службу**, ссылающуюся на Базу данных SQL Azure, хранилище данных SQL Azure или базу данных SQL Server, в которых следует запускать хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="40635-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="40635-3166">Выходной набор данных может использоваться для передачи результатов хранимой процедуры для дальнейшей обработки с помощью другого действия ([цепочки действий](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) в конвейере.</span><span class="sxs-lookup"><span data-stu-id="40635-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="40635-3167">Тем не менее фабрика данных не записывает выходные данные хранимой процедуры в этот набор данных автоматически.</span><span class="sxs-lookup"><span data-stu-id="40635-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="40635-3168">Выходные данные записывает сама хранимая процедура в таблицу SQL, на которую указывает выходной набор данных.</span><span class="sxs-lookup"><span data-stu-id="40635-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="40635-3169">В некоторых случаях выходной набор данных может быть **фиктивным набором данных**. Он используется, только чтобы задать расписание выполнения действия хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="40635-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="40635-3170">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3170">JSON example</span></span>

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

<span data-ttu-id="40635-3171">Дополнительные сведения см. в статье о [действии хранимой процедуры](data-factory-stored-proc-activity.md).</span><span class="sxs-lookup"><span data-stu-id="40635-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="40635-3172">Настраиваемое действие .NET</span><span class="sxs-lookup"><span data-stu-id="40635-3172">.NET custom activity</span></span>
<span data-ttu-id="40635-3173">В определении JSON настраиваемого действия .NET можно указать следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="40635-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="40635-3174">Свойству type присваивается значение **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="40635-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="40635-3175">Создайте связанную службу Azure HDInsight или связанную пакетную службу Azure и укажите ее имя в качестве значения свойства **linkedServiceName**.</span><span class="sxs-lookup"><span data-stu-id="40635-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="40635-3176">В разделе **typeProperties** при установке DotNetActivity в качестве типа действия поддерживаются следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="40635-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="40635-3177">Свойство</span><span class="sxs-lookup"><span data-stu-id="40635-3177">Property</span></span> | <span data-ttu-id="40635-3178">Описание</span><span class="sxs-lookup"><span data-stu-id="40635-3178">Description</span></span> | <span data-ttu-id="40635-3179">Обязательно</span><span class="sxs-lookup"><span data-stu-id="40635-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="40635-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="40635-3180">AssemblyName</span></span> | <span data-ttu-id="40635-3181">Имя сборки.</span><span class="sxs-lookup"><span data-stu-id="40635-3181">Name of the assembly.</span></span> <span data-ttu-id="40635-3182">В этом примере это **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="40635-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="40635-3183">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3183">Yes</span></span> |
| <span data-ttu-id="40635-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="40635-3184">EntryPoint</span></span> |<span data-ttu-id="40635-3185">Имя класса, реализующего интерфейс IDotNetActivity.</span><span class="sxs-lookup"><span data-stu-id="40635-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="40635-3186">В примере это **MyDotNetActivityNS.MyDotNetActivity**, где MyDotNetActivityNS — это пространство имен, а MyDotNetActivity — класс.</span><span class="sxs-lookup"><span data-stu-id="40635-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="40635-3187">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3187">Yes</span></span> | 
| <span data-ttu-id="40635-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="40635-3188">PackageLinkedService</span></span> | <span data-ttu-id="40635-3189">Имя связанной службы хранилища Azure, указывающей на хранилище BLOB-объектов с ZIP-файлом настраиваемого действия.</span><span class="sxs-lookup"><span data-stu-id="40635-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="40635-3190">В этом примере это **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="40635-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="40635-3191">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3191">Yes</span></span> |
| <span data-ttu-id="40635-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="40635-3192">PackageFile</span></span> | <span data-ttu-id="40635-3193">Имя ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="40635-3193">Name of the zip file.</span></span> <span data-ttu-id="40635-3194">В этом примере это **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="40635-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="40635-3195">Да</span><span class="sxs-lookup"><span data-stu-id="40635-3195">Yes</span></span> |
| <span data-ttu-id="40635-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="40635-3196">extendedProperties</span></span> | <span data-ttu-id="40635-3197">Расширенные свойства, которые можно определить и передать в код .NET.</span><span class="sxs-lookup"><span data-stu-id="40635-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="40635-3198">В этом примере переменной **SliceStart** присваивается значение на основе системной переменной SliceStart.</span><span class="sxs-lookup"><span data-stu-id="40635-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="40635-3199">Нет</span><span class="sxs-lookup"><span data-stu-id="40635-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="40635-3200">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="40635-3200">JSON example</span></span>

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

<span data-ttu-id="40635-3201">Подробные сведения см. в статье об [использовании настраиваемых действий в фабрике данных](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="40635-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="40635-3202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40635-3202">Next Steps</span></span>
<span data-ttu-id="40635-3203">Ознакомьтесь со следующими руководствами:</span><span class="sxs-lookup"><span data-stu-id="40635-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="40635-3204">Руководство. Создание конвейера с действием копирования с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="40635-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="40635-3205">Руководство. Создание первой фабрики данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="40635-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)