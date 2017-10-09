---
title: "запросы эффективный список aaaDesign - пакетной службы Azure | Документы Microsoft"
description: "Сведения о повышении производительности за счет фильтрации запросов, а именно при запросе сведений о ресурсах пакетной службы: пулах, заданиях, задачах и вычислительных узлах."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 031fefeb-248e-4d5a-9bc2-f07e46ddd30d
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 08/02/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b7e554119ec9d0e9e8007ccfb1ca80fe142a5e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-queries-toolist-batch-resources-efficiently"></a><span data-ttu-id="78513-103">Эффективно создавать запросы toolist пакета ресурсов</span><span class="sxs-lookup"><span data-stu-id="78513-103">Create queries toolist Batch resources efficiently</span></span>

<span data-ttu-id="78513-104">Здесь вы узнаете, как tooincrease производительность приложения пакетной службы Azure, уменьшая hello объем данных, возвращаемых службой hello при запросе заданий, задач и вычислительных узлов с hello [пакета .NET] [ api_net] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="78513-104">Here you'll learn how tooincrease your Azure Batch application's performance by reducing hello amount of data that is returned by hello service when you query jobs, tasks, and compute nodes with hello [Batch .NET][api_net] library.</span></span>

<span data-ttu-id="78513-105">Практически все приложения пакета должны tooperform некоторые типы операций мониторинга или другие запросы пакетная служба hello, часто через регулярные интервалы.</span><span class="sxs-lookup"><span data-stu-id="78513-105">Nearly all Batch applications need tooperform some type of monitoring or other operation that queries hello Batch service, often at regular intervals.</span></span> <span data-ttu-id="78513-106">Например, toodetermine являются ли все задачи в очереди, оставшихся в задании должен получить данные для каждой задачи в задании hello.</span><span class="sxs-lookup"><span data-stu-id="78513-106">For example, toodetermine whether there are any queued tasks remaining in a job, you must get data on every task in hello job.</span></span> <span data-ttu-id="78513-107">состояние hello toodetermine узлов в пул, необходимо получить данные на каждом узле в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="78513-107">toodetermine hello status of nodes in your pool, you must get data on every node in hello pool.</span></span> <span data-ttu-id="78513-108">В этой статье объясняется, как tooexecute такие запросы в hello наиболее эффективным способом.</span><span class="sxs-lookup"><span data-stu-id="78513-108">This article explains how tooexecute such queries in hello most efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="78513-109">Hello пакетная служба поддерживает специальные API распространенный сценарий hello подсчет задач в задании.</span><span class="sxs-lookup"><span data-stu-id="78513-109">hello Batch service provides special API support for hello common scenario of counting tasks in a job.</span></span> <span data-ttu-id="78513-110">Вместо этих запрос списка, можно вызвать hello [получить количество задач] [ rest_get_task_counts] операции.</span><span class="sxs-lookup"><span data-stu-id="78513-110">Instead of using a list query for these, you can call hello [Get Task Counts][rest_get_task_counts] operation.</span></span> <span data-ttu-id="78513-111">Эта операция указывает количество задач, ожидающих выполнения, запущенных, завершенных, успешно или неудачно выполненных задач.</span><span class="sxs-lookup"><span data-stu-id="78513-111">Get Task Counts indicates how many tasks are pending, running or complete, and how many tasks have succeeded or failed.</span></span> <span data-ttu-id="78513-112">Это операция эффективнее запроса списка.</span><span class="sxs-lookup"><span data-stu-id="78513-112">Get Task Counts is more efficient than a list query.</span></span> <span data-ttu-id="78513-113">Дополнительные сведения см. в статье [Подсчет задач по состоянию для мониторинга хода выполнения задания (предварительная версия)](batch-get-task-counts.md).</span><span class="sxs-lookup"><span data-stu-id="78513-113">For more information, see [Count tasks for a job by state (Preview)](batch-get-task-counts.md).</span></span> 
>
> <span data-ttu-id="78513-114">Hello получить количество задач операция недоступна в версии пакета обновления более ранней, чем 2017 г-06-01.5.1.</span><span class="sxs-lookup"><span data-stu-id="78513-114">hello Get Task Counts operation is not available in Batch service versions earlier than 2017-06-01.5.1.</span></span> <span data-ttu-id="78513-115">Если вы используете старую версию службы hello, затем используйте задачи toocount список запросов в задании.</span><span class="sxs-lookup"><span data-stu-id="78513-115">If you are using an older version of hello service, then use a list query toocount tasks in a job instead.</span></span>
>
> 

## <a name="meet-hello-detaillevel"></a><span data-ttu-id="78513-116">Соответствует hello DetailLevel</span><span class="sxs-lookup"><span data-stu-id="78513-116">Meet hello DetailLevel</span></span>
<span data-ttu-id="78513-117">В рабочей среде пакета приложения пронумеровать сущности, такие как задания, задач и вычислительных узлов можно hello тысяч.</span><span class="sxs-lookup"><span data-stu-id="78513-117">In a production Batch application, entities like jobs, tasks, and compute nodes can number in hello thousands.</span></span> <span data-ttu-id="78513-118">При запросе сведения о таких ресурсах потенциально большой объем данных должен» cross передачи hello» из службы tooyour hello пакета приложения на каждый запрос.</span><span class="sxs-lookup"><span data-stu-id="78513-118">When you request information on these resources, a potentially large amount of data must "cross hello wire" from hello Batch service tooyour application on each query.</span></span> <span data-ttu-id="78513-119">Ограничивая hello число элементов и тип данных, возвращаемых запросом, может увеличить hello ускорения обработки запросов и поэтому hello производительности приложения.</span><span class="sxs-lookup"><span data-stu-id="78513-119">By limiting hello number of items and type of information that is returned by a query, you can increase hello speed of your queries, and therefore hello performance of your application.</span></span>

<span data-ttu-id="78513-120">Это [пакета .NET] [ api_net] списки фрагментов кода API *каждого* задач, связанных с заданием, вместе с *все* hello свойств каждого задача.</span><span class="sxs-lookup"><span data-stu-id="78513-120">This [Batch .NET][api_net] API code snippet lists *every* task that is associated with a job, along with *all* of hello properties of each task:</span></span>

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

<span data-ttu-id="78513-121">Запрос списка намного более эффективным, тем не менее, можно выполнить путем применения запроса tooyour «уровень детализации».</span><span class="sxs-lookup"><span data-stu-id="78513-121">You can perform a much more efficient list query, however, by applying a "detail level" tooyour query.</span></span> <span data-ttu-id="78513-122">Это делается путем указания [ODATADetailLevel] [ odata] объекта toohello [JobOperations.ListTasks] [ net_list_tasks] метод.</span><span class="sxs-lookup"><span data-stu-id="78513-122">You do this by supplying an [ODATADetailLevel][odata] object toohello [JobOperations.ListTasks][net_list_tasks] method.</span></span> <span data-ttu-id="78513-123">Этот фрагмент возвращает только идентификатор hello, командной строки, вычислений свойства узла и сведения о завершенных задач:</span><span class="sxs-lookup"><span data-stu-id="78513-123">This snippet returns only hello ID, command line, and compute node information properties of completed tasks:</span></span>

```csharp
// Configure an ODATADetailLevel specifying a subset of tasks and
// their properties tooreturn
ODATADetailLevel detailLevel = new ODATADetailLevel();
detailLevel.FilterClause = "state eq 'completed'";
detailLevel.SelectClause = "id,commandLine,nodeInfo";

// Supply hello ODATADetailLevel toohello ListTasks method
IPagedEnumerable<CloudTask> completedTasks =
    batchClient.JobOperations.ListTasks("job-001", detailLevel);
```

<span data-ttu-id="78513-124">В этом примере сценария, если существуют тысячи задачи в задании hello hello результаты из второго запроса hello обычно будут возвращены первыми намного быстрее, чем hello.</span><span class="sxs-lookup"><span data-stu-id="78513-124">In this example scenario, if there are thousands of tasks in hello job, hello results from hello second query will typically be returned much quicker than hello first.</span></span> <span data-ttu-id="78513-125">Дополнительные сведения об использовании ODATADetailLevel при перечислении элементов с помощью пакета .NET API hello включено [ниже](#efficient-querying-in-batch-net).</span><span class="sxs-lookup"><span data-stu-id="78513-125">More information about using ODATADetailLevel when you list items with hello Batch .NET API is included [below](#efficient-querying-in-batch-net).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78513-126">Настоятельно рекомендуется, чтобы вы *всегда* введите список .NET API tooyour ODATADetailLevel объекта вызывает tooensure Максимальная эффективность и производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="78513-126">We highly recommend that you *always* supply an ODATADetailLevel object tooyour .NET API list calls tooensure maximum efficiency and performance of your application.</span></span> <span data-ttu-id="78513-127">Если задать уровень детализации, может помочь toolower пакетной службы времени отклика, повысить эффективность использования сети и свести к минимуму использование памяти клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="78513-127">By specifying a detail level, you can help toolower Batch service response times, improve network utilization, and minimize memory usage by client applications.</span></span>
> 
> 

## <a name="filter-select-and-expand"></a><span data-ttu-id="78513-128">Фильтрация, выборка и развертывание</span><span class="sxs-lookup"><span data-stu-id="78513-128">Filter, select, and expand</span></span>
<span data-ttu-id="78513-129">Hello [пакета .NET] [ api_net] и [REST пакетной] [ api_rest] API обеспечивают возможность tooreduce hello обоих hello число элементов, которые возвращаются в виде списка а также объем сведений, возвращаемых для каждой hello.</span><span class="sxs-lookup"><span data-stu-id="78513-129">hello [Batch .NET][api_net] and [Batch REST][api_rest] APIs provide hello ability tooreduce both hello number of items that are returned in a list, as well as hello amount of information that is returned for each.</span></span> <span data-ttu-id="78513-130">Для этого в запросе необходимо указать строки **фильтрации**, **выборки** и **развертывания**.</span><span class="sxs-lookup"><span data-stu-id="78513-130">You do so by specifying **filter**, **select**, and **expand strings** when performing list queries.</span></span>

### <a name="filter"></a><span data-ttu-id="78513-131">Фильтр</span><span class="sxs-lookup"><span data-stu-id="78513-131">Filter</span></span>
<span data-ttu-id="78513-132">Строка Hello фильтра — это выражение, уменьшает количество элементов, возвращаемых в hello.</span><span class="sxs-lookup"><span data-stu-id="78513-132">hello filter string is an expression that reduces hello number of items that are returned.</span></span> <span data-ttu-id="78513-133">Например список только hello выполняемые задачи для задания или список только вычислительных узлов, которые готовы toorun задачи.</span><span class="sxs-lookup"><span data-stu-id="78513-133">For example, list only hello running tasks for a job, or list only compute nodes that are ready toorun tasks.</span></span>

* <span data-ttu-id="78513-134">Строка Hello фильтра состоит из одного или нескольких выражений, с помощью выражения, которая состоит из имени свойства, оператор и значение.</span><span class="sxs-lookup"><span data-stu-id="78513-134">hello filter string consists of one or more expressions, with an expression that consists of a property name, operator, and value.</span></span> <span data-ttu-id="78513-135">Hello свойства, которые могут быть указаны являются tooeach определенного типа сущности, который вы выполняете запрос, hello операторы, которые поддерживаются для каждого свойства.</span><span class="sxs-lookup"><span data-stu-id="78513-135">hello properties that can be specified are specific tooeach entity type that you query, as are hello operators that are supported for each property.</span></span>
* <span data-ttu-id="78513-136">Несколько выражений, которые могут быть объединены с помощью логических операторов hello `and` и `or`.</span><span class="sxs-lookup"><span data-stu-id="78513-136">Multiple expressions can be combined by using hello logical operators `and` and `or`.</span></span>
* <span data-ttu-id="78513-137">В этом примере фильтрация списков строк только под управлением hello «визуализации» задачи: `(state eq 'running') and startswith(id, 'renderTask')`.</span><span class="sxs-lookup"><span data-stu-id="78513-137">This example filter string lists only hello running "render" tasks: `(state eq 'running') and startswith(id, 'renderTask')`.</span></span>

### <a name="select"></a><span data-ttu-id="78513-138">Выберите пункт</span><span class="sxs-lookup"><span data-stu-id="78513-138">Select</span></span>
<span data-ttu-id="78513-139">Выберите строку Hello ограничивает hello значения свойств, которые возвращаются для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="78513-139">hello select string limits hello property values that are returned for each item.</span></span> <span data-ttu-id="78513-140">Укажите список имен свойств и для элементов hello в результатах запроса hello возвращаются только те значения свойства.</span><span class="sxs-lookup"><span data-stu-id="78513-140">You specify a list of property names, and only those property values are returned for hello items in hello query results.</span></span>

* <span data-ttu-id="78513-141">Выберите строку Hello состоит из разделенных запятыми список имен свойств.</span><span class="sxs-lookup"><span data-stu-id="78513-141">hello select string consists of a comma-separated list of property names.</span></span> <span data-ttu-id="78513-142">Можно указать любую hello свойств для типа сущности hello, выполнении запроса.</span><span class="sxs-lookup"><span data-stu-id="78513-142">You can specify any of hello properties for hello entity type you are querying.</span></span>
* <span data-ttu-id="78513-143">В этом примере строка выборки указывает, что для каждой задачи необходимо вернуть значения только трех свойств: `id, state, stateTransitionTime`.</span><span class="sxs-lookup"><span data-stu-id="78513-143">This example select string specifies that only three property values should be returned for each task: `id, state, stateTransitionTime`.</span></span>

### <a name="expand"></a><span data-ttu-id="78513-144">Разверните</span><span class="sxs-lookup"><span data-stu-id="78513-144">Expand</span></span>
<span data-ttu-id="78513-145">Hello разверните строку уменьшает число hello вызовы API, необходимые tooobtain определенные сведения.</span><span class="sxs-lookup"><span data-stu-id="78513-145">hello expand string reduces hello number of API calls that are required tooobtain certain information.</span></span> <span data-ttu-id="78513-146">При использовании строки развертывания дополнительные сведения о каждом элементе можно получить с помощью одного вызова API.</span><span class="sxs-lookup"><span data-stu-id="78513-146">When you use an expand string, more information about each item can be obtained with a single API call.</span></span> <span data-ttu-id="78513-147">Вместо того чтобы первого получения hello список сущностей, а затем запросом сведений для каждого элемента в списке hello, используйте строку развернуть tooobtain hello одинаковые данные в одном вызове API.</span><span class="sxs-lookup"><span data-stu-id="78513-147">Rather than first obtaining hello list of entities, then requesting information for each item in hello list, you use an expand string tooobtain hello same information in a single API call.</span></span> <span data-ttu-id="78513-148">Чем меньше вызовов API, тем выше производительность.</span><span class="sxs-lookup"><span data-stu-id="78513-148">Less API calls means better performance.</span></span>

* <span data-ttu-id="78513-149">Аналогичные toohello выберите строку, hello разверните элементы управления строки ли определенные данные включаются в список результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="78513-149">Similar toohello select string, hello expand string controls whether certain data is included in list query results.</span></span>
* <span data-ttu-id="78513-150">Hello разверните строку поддерживается только в том случае, когда он используется в список заданий, расписаний заданий, задач и пулы.</span><span class="sxs-lookup"><span data-stu-id="78513-150">hello expand string is only supported when it is used in listing jobs, job schedules, tasks, and pools.</span></span> <span data-ttu-id="78513-151">В настоящее время они поддерживают только статистические данные.</span><span class="sxs-lookup"><span data-stu-id="78513-151">Currently, it only supports statistics information.</span></span>
* <span data-ttu-id="78513-152">Если необходимы все свойства и выберите Строка не указана, hello разверните строку *должен* быть используется tooget статистические данные.</span><span class="sxs-lookup"><span data-stu-id="78513-152">When all properties are required and no select string is specified, hello expand string *must* be used tooget statistics information.</span></span> <span data-ttu-id="78513-153">Если строка select — используется tooobtain подмножество свойств, затем `stats` может задаваться в строке выберите hello и hello разверните строку не требуется toobe указано.</span><span class="sxs-lookup"><span data-stu-id="78513-153">If a select string is used tooobtain a subset of properties, then `stats` can be specified in hello select string, and hello expand string does not need toobe specified.</span></span>
* <span data-ttu-id="78513-154">В этом примере разверните строка указывает, что статистические данные должны быть возвращены для каждого элемента в списке hello: `stats`.</span><span class="sxs-lookup"><span data-stu-id="78513-154">This example expand string specifies that statistics information should be returned for each item in hello list: `stats`.</span></span>

> [!NOTE]
> <span data-ttu-id="78513-155">При создании любого hello три запроса строковые типы (фильтрации, выберите и разверните), необходимо убедиться, имена свойств hello и case совпадали с их аналогами элемент интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="78513-155">When constructing any of hello three query string types (filter, select, and expand), you must ensure that hello property names and case match that of their REST API element counterparts.</span></span> <span data-ttu-id="78513-156">Например, при работе с hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) , необходимо указать **состояние** вместо **состояние**, даже если hello свойство .NET — [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span><span class="sxs-lookup"><span data-stu-id="78513-156">For example, when working with hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) class, you must specify **state** instead of **State**, even though hello .NET property is [CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state).</span></span> <span data-ttu-id="78513-157">В разделе hello таблицы ниже для сопоставления свойств между hello .NET и API-интерфейсов REST.</span><span class="sxs-lookup"><span data-stu-id="78513-157">See hello tables below for property mappings between hello .NET and REST APIs.</span></span>
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a><span data-ttu-id="78513-158">Правила строк фильтрации, выборки и развертывания</span><span class="sxs-lookup"><span data-stu-id="78513-158">Rules for filter, select, and expand strings</span></span>
* <span data-ttu-id="78513-159">Имена свойств в фильтре, выберите и разверните строк должны отображаться как в hello [REST пакетной] [ api_rest] API — даже при использовании [пакета .NET] [ api_net] или одного из других пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="78513-159">Properties names in filter, select, and expand strings should appear as they do in hello [Batch REST][api_rest] API--even when you use [Batch .NET][api_net] or one of hello other Batch SDKs.</span></span>
* <span data-ttu-id="78513-160">Имена всех свойств чувствительны к регистру, но для значений свойств регистр значения не имеет.</span><span class="sxs-lookup"><span data-stu-id="78513-160">All property names are case-sensitive, but property values are case insensitive.</span></span>
* <span data-ttu-id="78513-161">Строки даты и времени могут иметь один из двух форматов и должны начинаться с `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="78513-161">Date/time strings can be one of two formats, and must be preceded with `DateTime`.</span></span>
  
  * <span data-ttu-id="78513-162">Пример формата W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span><span class="sxs-lookup"><span data-stu-id="78513-162">W3C-DTF format example: `creationTime gt DateTime'2011-05-08T08:49:37Z'`</span></span>
  * <span data-ttu-id="78513-163">Пример формата RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span><span class="sxs-lookup"><span data-stu-id="78513-163">RFC 1123 format example: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`</span></span>
* <span data-ttu-id="78513-164">Строки с логическими выражениями должны иметь значение `true` или `false`.</span><span class="sxs-lookup"><span data-stu-id="78513-164">Boolean strings are either `true` or `false`.</span></span>
* <span data-ttu-id="78513-165">Если задано недопустимое свойство или оператор, отобразится ошибка `400 (Bad Request)` .</span><span class="sxs-lookup"><span data-stu-id="78513-165">If an invalid property or operator is specified, a `400 (Bad Request)` error will result.</span></span>

## <a name="efficient-querying-in-batch-net"></a><span data-ttu-id="78513-166">Эффективное выполнение запросов в пакетной службе для .NET</span><span class="sxs-lookup"><span data-stu-id="78513-166">Efficient querying in Batch .NET</span></span>
<span data-ttu-id="78513-167">В рамках hello [пакета .NET] [ api_net] API, hello [ODATADetailLevel] [ odata] класс используется для указания фильтра, выберите и разверните строк toolist операции.</span><span class="sxs-lookup"><span data-stu-id="78513-167">Within hello [Batch .NET][api_net] API, hello [ODATADetailLevel][odata] class is used for supplying filter, select, and expand strings toolist operations.</span></span> <span data-ttu-id="78513-168">Hello ODataDetailLevel класс имеет три строку открытого свойства, которые могут быть определены в конструкторе hello, или задать непосредственно hello объекта.</span><span class="sxs-lookup"><span data-stu-id="78513-168">hello ODataDetailLevel class has three public string properties that can be specified in hello constructor, or set directly on hello object.</span></span> <span data-ttu-id="78513-169">Затем передается hello ODataDetailLevel объект как toohello параметр различные операции списка таких как [ListPools][net_list_pools], [ListJobs][net_list_jobs], и [ListTasks][net_list_tasks].</span><span class="sxs-lookup"><span data-stu-id="78513-169">You then pass hello ODataDetailLevel object as a parameter toohello various list operations such as [ListPools][net_list_pools], [ListJobs][net_list_jobs], and [ListTasks][net_list_tasks].</span></span>

* <span data-ttu-id="78513-170">[ODATADetailLevel][odata].[ FilterClause][odata_filter]: максимальное число элементов, возвращаемых hello.</span><span class="sxs-lookup"><span data-stu-id="78513-170">[ODATADetailLevel][odata].[FilterClause][odata_filter]: Limit hello number of items that are returned.</span></span>
* <span data-ttu-id="78513-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: определяет, значения каких свойств необходимо вернуть для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="78513-171">[ODATADetailLevel][odata].[SelectClause][odata_select]: Specify which property values are returned with each item.</span></span>
* <span data-ttu-id="78513-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: извлекает данные по всем элементам за один вызов API вместо того, чтобы выполнять отдельные вызовы для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="78513-172">[ODATADetailLevel][odata].[ExpandClause][odata_expand]: Retrieve data for all items in a single API call instead of separate calls for each item.</span></span>

<span data-ttu-id="78513-173">Hello следующий фрагмент кода hello пакета .NET API tooefficiently запроса hello пакета служба используется для статистики hello определенного набора пулов.</span><span class="sxs-lookup"><span data-stu-id="78513-173">hello following code snippet uses hello Batch .NET API tooefficiently query hello Batch service for hello statistics of a specific set of pools.</span></span> <span data-ttu-id="78513-174">В этом сценарии hello пакета пользователем тестовой и рабочей группы.</span><span class="sxs-lookup"><span data-stu-id="78513-174">In this scenario, hello Batch user has both test and production pools.</span></span> <span data-ttu-id="78513-175">Hello теста пул идентификаторов имеют префикс «test» и hello Производственный кластер идентификаторы имеют префикс «prod».</span><span class="sxs-lookup"><span data-stu-id="78513-175">hello test pool IDs are prefixed with "test", and hello production pool IDs are prefixed with "prod".</span></span> <span data-ttu-id="78513-176">Во фрагменте hello *myBatchClient* — это правильно инициализированный экземпляр hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) класса.</span><span class="sxs-lookup"><span data-stu-id="78513-176">In hello snippet, *myBatchClient* is a properly initialized instance of hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) class.</span></span>

```csharp
// First we need an ODATADetailLevel instance on which tooset hello filter, select,
// and expand clause strings
ODATADetailLevel detailLevel = new ODATADetailLevel();

// We want toopull only hello "test" pools, so we limit hello number of items returned
// by using a FilterClause and specifying that hello pool IDs must start with "test"
detailLevel.FilterClause = "startswith(id, 'test')";

// toofurther limit hello data that crosses hello wire, configure hello SelectClause to
// limit hello properties that are returned on each CloudPool object tooonly
// CloudPool.Id and CloudPool.Statistics
detailLevel.SelectClause = "id, stats";

// Specify hello ExpandClause so that hello .NET API pulls hello statistics for the
// CloudPools in a single underlying REST API call. Note that we use hello pool's
// REST API element name "stats" here as opposed too"Statistics" as it appears in
// hello .NET API (CloudPool.Statistics)
detailLevel.ExpandClause = "stats";

// Now get our collection of pools, minimizing hello amount of data that is returned
// by specifying hello detail level that we configured above
List<CloudPool> testPools =
    await myBatchClient.PoolOperations.ListPools(detailLevel).ToListAsync();
```

> [!TIP]
> <span data-ttu-id="78513-177">Экземпляр [ODATADetailLevel] [ odata] , настроенный с помощью Select и Expand предложений также можно передать методы Get tooappropriate, такие как [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit hello объем возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="78513-177">An instance of [ODATADetailLevel][odata] that is configured with Select and Expand clauses can also be passed tooappropriate Get methods, such as [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx), toolimit hello amount of data that is returned.</span></span>
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a><span data-ttu-id="78513-178">Сопоставления REST too.NET API пакета</span><span class="sxs-lookup"><span data-stu-id="78513-178">Batch REST too.NET API mappings</span></span>
<span data-ttu-id="78513-179">Имена и регистр свойств в строках фильтрации, выборки и развертывания *должны* полностью соответствовать аналогичным элементам в REST API.</span><span class="sxs-lookup"><span data-stu-id="78513-179">Property names in filter, select, and expand strings *must* reflect their REST API counterparts, both in name and case.</span></span> <span data-ttu-id="78513-180">Hello ниже приведены сопоставления между hello .NET и API-интерфейса REST эквивалентами.</span><span class="sxs-lookup"><span data-stu-id="78513-180">hello tables below provide mappings between hello .NET and REST API counterparts.</span></span>

### <a name="mappings-for-filter-strings"></a><span data-ttu-id="78513-181">Сопоставления для строк фильтрации</span><span class="sxs-lookup"><span data-stu-id="78513-181">Mappings for filter strings</span></span>
* <span data-ttu-id="78513-182">**Список методов .NET**: каждый из методов .NET API hello в этом столбце принимает [ODATADetailLevel] [ odata] объект в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="78513-182">**.NET list methods**: Each of hello .NET API methods in this column accepts an [ODATADetailLevel][odata] object as a parameter.</span></span>
* <span data-ttu-id="78513-183">**Список запросов REST**: каждый API REST страницы связанного tooin этот столбец содержит таблицу, которая задает свойства hello и операции, допустимых в *фильтра* строки.</span><span class="sxs-lookup"><span data-stu-id="78513-183">**REST list requests**: Each REST API page linked tooin this column contains a table that specifies hello properties and operations that are allowed in *filter* strings.</span></span> <span data-ttu-id="78513-184">Эти имена свойств и операции будут использоваться при создании строки [ODATADetailLevel.FilterClause][odata_filter].</span><span class="sxs-lookup"><span data-stu-id="78513-184">You will use these property names and operations when you construct an [ODATADetailLevel.FilterClause][odata_filter] string.</span></span>

| <span data-ttu-id="78513-185">Методы списка .NET</span><span class="sxs-lookup"><span data-stu-id="78513-185">.NET list methods</span></span> | <span data-ttu-id="78513-186">Запросы списка REST</span><span class="sxs-lookup"><span data-stu-id="78513-186">REST list requests</span></span> |
| --- | --- |
| <span data-ttu-id="78513-187">[CertificateOperations.ListCertificates][net_list_certs]</span><span class="sxs-lookup"><span data-stu-id="78513-187">[CertificateOperations.ListCertificates][net_list_certs]</span></span> |<span data-ttu-id="78513-188">[Список сертификатов hello в учетной записи][rest_list_certs]</span><span class="sxs-lookup"><span data-stu-id="78513-188">[List hello certificates in an account][rest_list_certs]</span></span> |
| <span data-ttu-id="78513-189">[CloudTask.ListNodeFiles][net_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="78513-189">[CloudTask.ListNodeFiles][net_list_task_files]</span></span> |<span data-ttu-id="78513-190">[Список файлов hello, связанного с задачей][rest_list_task_files]</span><span class="sxs-lookup"><span data-stu-id="78513-190">[List hello files associated with a task][rest_list_task_files]</span></span> |
| <span data-ttu-id="78513-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="78513-191">[JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status]</span></span> |<span data-ttu-id="78513-192">[Отображение состояния hello hello подготовки задания и задания выпуска задачи для задания][rest_list_jobprep_status]</span><span class="sxs-lookup"><span data-stu-id="78513-192">[List hello status of hello job preparation and job release tasks for a job][rest_list_jobprep_status]</span></span> |
| <span data-ttu-id="78513-193">[JobOperations.ListJobs][net_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="78513-193">[JobOperations.ListJobs][net_list_jobs]</span></span> |<span data-ttu-id="78513-194">[Перечисление заданий hello в учетной записи][rest_list_jobs]</span><span class="sxs-lookup"><span data-stu-id="78513-194">[List hello jobs in an account][rest_list_jobs]</span></span> |
| <span data-ttu-id="78513-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="78513-195">[JobOperations.ListNodeFiles][net_list_nodefiles]</span></span> |<span data-ttu-id="78513-196">[Список файлов hello на узле][rest_list_nodefiles]</span><span class="sxs-lookup"><span data-stu-id="78513-196">[List hello files on a node][rest_list_nodefiles]</span></span> |
| <span data-ttu-id="78513-197">[JobOperations.ListTasks][net_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="78513-197">[JobOperations.ListTasks][net_list_tasks]</span></span> |<span data-ttu-id="78513-198">[Список задач hello, связанных с заданием][rest_list_tasks]</span><span class="sxs-lookup"><span data-stu-id="78513-198">[List hello tasks associated with a job][rest_list_tasks]</span></span> |
| <span data-ttu-id="78513-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="78513-199">[JobScheduleOperations.ListJobSchedules][net_list_job_schedules]</span></span> |<span data-ttu-id="78513-200">[Список расписаний заданий hello в учетной записи][rest_list_job_schedules]</span><span class="sxs-lookup"><span data-stu-id="78513-200">[List hello job schedules in an account][rest_list_job_schedules]</span></span> |
| <span data-ttu-id="78513-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="78513-201">[JobScheduleOperations.ListJobs][net_list_schedule_jobs]</span></span> |<span data-ttu-id="78513-202">[Список заданий hello, связанных с расписания задания][rest_list_schedule_jobs]</span><span class="sxs-lookup"><span data-stu-id="78513-202">[List hello jobs associated with a job schedule][rest_list_schedule_jobs]</span></span> |
| <span data-ttu-id="78513-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="78513-203">[PoolOperations.ListComputeNodes][net_list_compute_nodes]</span></span> |<span data-ttu-id="78513-204">[Список hello вычислительных узлов в пуле][rest_list_compute_nodes]</span><span class="sxs-lookup"><span data-stu-id="78513-204">[List hello compute nodes in a pool][rest_list_compute_nodes]</span></span> |
| <span data-ttu-id="78513-205">[PoolOperations.ListPools][net_list_pools]</span><span class="sxs-lookup"><span data-stu-id="78513-205">[PoolOperations.ListPools][net_list_pools]</span></span> |<span data-ttu-id="78513-206">[Список пулов hello в учетной записи][rest_list_pools]</span><span class="sxs-lookup"><span data-stu-id="78513-206">[List hello pools in an account][rest_list_pools]</span></span> |

### <a name="mappings-for-select-strings"></a><span data-ttu-id="78513-207">Сопоставления для строк выборки</span><span class="sxs-lookup"><span data-stu-id="78513-207">Mappings for select strings</span></span>
* <span data-ttu-id="78513-208">**Типы пакетной службы для .NET**— типы API пакетной службы для .NET.</span><span class="sxs-lookup"><span data-stu-id="78513-208">**Batch .NET types**: Batch .NET API types.</span></span>
* <span data-ttu-id="78513-209">**Сущности REST API**: каждая страница в этот столбец содержит одну или несколько таблиц, в которых перечислены имена свойств hello REST API для типа hello.</span><span class="sxs-lookup"><span data-stu-id="78513-209">**REST API entities**: Each page in this column contains one or more tables that list hello REST API property names for hello type.</span></span> <span data-ttu-id="78513-210">Эти имена свойств используются при создании строк *выборки* .</span><span class="sxs-lookup"><span data-stu-id="78513-210">These property names are used when you construct *select* strings.</span></span> <span data-ttu-id="78513-211">Они также будут использоваться при создании строки [ODATADetailLevel.SelectClause][odata_select].</span><span class="sxs-lookup"><span data-stu-id="78513-211">You will use these same property names when you construct an [ODATADetailLevel.SelectClause][odata_select] string.</span></span>

| <span data-ttu-id="78513-212">Типы пакетной службы для .NET</span><span class="sxs-lookup"><span data-stu-id="78513-212">Batch .NET types</span></span> | <span data-ttu-id="78513-213">Сущности REST API</span><span class="sxs-lookup"><span data-stu-id="78513-213">REST API entities</span></span> |
| --- | --- |
| <span data-ttu-id="78513-214">[Certificate][net_cert]</span><span class="sxs-lookup"><span data-stu-id="78513-214">[Certificate][net_cert]</span></span> |<span data-ttu-id="78513-215">[Получение информации о сертификате][rest_get_cert]</span><span class="sxs-lookup"><span data-stu-id="78513-215">[Get information about a certificate][rest_get_cert]</span></span> |
| <span data-ttu-id="78513-216">[CloudJob][net_job]</span><span class="sxs-lookup"><span data-stu-id="78513-216">[CloudJob][net_job]</span></span> |<span data-ttu-id="78513-217">[Получение информации о задании][rest_get_job]</span><span class="sxs-lookup"><span data-stu-id="78513-217">[Get information about a job][rest_get_job]</span></span> |
| <span data-ttu-id="78513-218">[CloudJobSchedule][net_schedule]</span><span class="sxs-lookup"><span data-stu-id="78513-218">[CloudJobSchedule][net_schedule]</span></span> |<span data-ttu-id="78513-219">[Получение информации о расписании задания][rest_get_schedule]</span><span class="sxs-lookup"><span data-stu-id="78513-219">[Get information about a job schedule][rest_get_schedule]</span></span> |
| <span data-ttu-id="78513-220">[ComputeNode][net_node]</span><span class="sxs-lookup"><span data-stu-id="78513-220">[ComputeNode][net_node]</span></span> |<span data-ttu-id="78513-221">[Получение информации об узле][rest_get_node]</span><span class="sxs-lookup"><span data-stu-id="78513-221">[Get information about a node][rest_get_node]</span></span> |
| <span data-ttu-id="78513-222">[CloudPool][net_pool]</span><span class="sxs-lookup"><span data-stu-id="78513-222">[CloudPool][net_pool]</span></span> |<span data-ttu-id="78513-223">[Получение информации о пуле][rest_get_pool]</span><span class="sxs-lookup"><span data-stu-id="78513-223">[Get information about a pool][rest_get_pool]</span></span> |
| <span data-ttu-id="78513-224">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="78513-224">[CloudTask][net_task]</span></span> |<span data-ttu-id="78513-225">[Получение информации о задаче][rest_get_task]</span><span class="sxs-lookup"><span data-stu-id="78513-225">[Get information about a task][rest_get_task]</span></span> |

## <a name="example-construct-a-filter-string"></a><span data-ttu-id="78513-226">Пример. Создание строки фильтрации</span><span class="sxs-lookup"><span data-stu-id="78513-226">Example: construct a filter string</span></span>
<span data-ttu-id="78513-227">При построении строку фильтра для [ODATADetailLevel.FilterClause][odata_filter], обратитесь к таблице hello выше в разделе «Сопоставлений для фильтрации строк» toofind hello API-интерфейса REST страницы документации, которая соответствует операции вывода списка toohello обратиться в tooperform.</span><span class="sxs-lookup"><span data-stu-id="78513-227">When you construct a filter string for [ODATADetailLevel.FilterClause][odata_filter], consult hello table above under "Mappings for filter strings" toofind hello REST API documentation page that corresponds toohello list operation that you wish tooperform.</span></span> <span data-ttu-id="78513-228">В первой таблице многострочные hello на этой странице можно найти hello фильтруемых свойств и их поддерживаемые операторы.</span><span class="sxs-lookup"><span data-stu-id="78513-228">You will find hello filterable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="78513-229">При желании tooretrieve все задачи, код выхода был ненулевое значение, например, это строк на [список hello задач, связанных с заданием] [ rest_list_tasks] задает строку применимым свойством hello и допустимые операторы:</span><span class="sxs-lookup"><span data-stu-id="78513-229">If you wish tooretrieve all tasks whose exit code was nonzero, for example, this row on [List hello tasks associated with a job][rest_list_tasks] specifies hello applicable property string and allowable operators:</span></span>

| <span data-ttu-id="78513-230">Свойство</span><span class="sxs-lookup"><span data-stu-id="78513-230">Property</span></span> | <span data-ttu-id="78513-231">Разрешенные операции</span><span class="sxs-lookup"><span data-stu-id="78513-231">Operations allowed</span></span> | <span data-ttu-id="78513-232">Тип</span><span class="sxs-lookup"><span data-stu-id="78513-232">Type</span></span> |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

<span data-ttu-id="78513-233">Таким образом будет hello строку фильтра для перечисления всех задач с ненулевой код выхода:</span><span class="sxs-lookup"><span data-stu-id="78513-233">Thus, hello filter string for listing all tasks with a nonzero exit code would be:</span></span>

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a><span data-ttu-id="78513-234">Пример. Создание строки выборки</span><span class="sxs-lookup"><span data-stu-id="78513-234">Example: construct a select string</span></span>
<span data-ttu-id="78513-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], обратитесь к таблице hello выше в разделе «Сопоставлений для выбора строк» и перейти страницу toohello REST API, соответствующий toohello тип сущности, которые списка.</span><span class="sxs-lookup"><span data-stu-id="78513-235">tooconstruct [ODATADetailLevel.SelectClause][odata_select], consult hello table above under "Mappings for select strings" and navigate toohello REST API page that corresponds toohello type of entity that you are listing.</span></span> <span data-ttu-id="78513-236">В первой таблице многострочные hello на этой странице можно найти доступный для выбора свойств hello и их поддерживаемые операторы.</span><span class="sxs-lookup"><span data-stu-id="78513-236">You will find hello selectable properties and their supported operators in hello first multirow table on that page.</span></span> <span data-ttu-id="78513-237">Желанию tooretrieve только идентификатор hello и командную строку для каждой задачи в списке, например, можно найти эти строки в таблице применимо hello на [получить сведения о задаче][rest_get_task]:</span><span class="sxs-lookup"><span data-stu-id="78513-237">If you wish tooretrieve only hello ID and command line for each task in a list, for example, you will find these rows in hello applicable table on [Get information about a task][rest_get_task]:</span></span>

| <span data-ttu-id="78513-238">Свойство</span><span class="sxs-lookup"><span data-stu-id="78513-238">Property</span></span> | <span data-ttu-id="78513-239">Тип</span><span class="sxs-lookup"><span data-stu-id="78513-239">Type</span></span> | <span data-ttu-id="78513-240">Примечания</span><span class="sxs-lookup"><span data-stu-id="78513-240">Notes</span></span> |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

<span data-ttu-id="78513-241">Выберите строку Hello для включения только идентификатор hello и командной строки с каждой из перечисленных задач будет следующим:</span><span class="sxs-lookup"><span data-stu-id="78513-241">hello select string for including only hello ID and command line with each listed task would then be:</span></span>

`id, commandLine`

## <a name="code-samples"></a><span data-ttu-id="78513-242">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="78513-242">Code samples</span></span>
### <a name="efficient-list-queries-code-sample"></a><span data-ttu-id="78513-243">Пример кода с эффективными запросами списков</span><span class="sxs-lookup"><span data-stu-id="78513-243">Efficient list queries code sample</span></span>
<span data-ttu-id="78513-244">Извлечение hello [EfficientListQueries] [ efficient_query_sample] примера проекта на GitHub toosee эффективность список запросов может повлиять на производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="78513-244">Check out hello [EfficientListQueries][efficient_query_sample] sample project on GitHub toosee how efficient list querying can affect performance in an application.</span></span> <span data-ttu-id="78513-245">Это консольное приложение C# создается и добавляется большое количество задач tooa задания.</span><span class="sxs-lookup"><span data-stu-id="78513-245">This C# console application creates and adds a large number of tasks tooa job.</span></span> <span data-ttu-id="78513-246">Затем, выполняются несколько вызовов toohello [JobOperations.ListTasks] [ net_list_tasks] метод и передает [ODATADetailLevel] [ odata] объекты, которые являются настроить другое свойство значения toovary hello объем возвращаемых toobe данных.</span><span class="sxs-lookup"><span data-stu-id="78513-246">Then, it makes multiple calls toohello [JobOperations.ListTasks][net_list_tasks] method and passes [ODATADetailLevel][odata] objects that are configured with different property values toovary hello amount of data toobe returned.</span></span> <span data-ttu-id="78513-247">Она дает примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="78513-247">It produces output similar toohello following:</span></span>

```
Adding 5000 tasks toojob jobEffQuery...
5000 tasks added in 00:00:47.3467587, hit ENTER tooquery tasks...

4943 tasks retrieved in 00:00:04.3408081 (ExpandClause:  | FilterClause: state eq 'active' | SelectClause: id,state)
0 tasks retrieved in 00:00:00.2662920 (ExpandClause:  | FilterClause: state eq 'running' | SelectClause: id,state)
59 tasks retrieved in 00:00:00.3337760 (ExpandClause:  | FilterClause: state eq 'completed' | SelectClause: id,state)
5000 tasks retrieved in 00:00:04.1429881 (ExpandClause:  | FilterClause:  | SelectClause: id,state)
5000 tasks retrieved in 00:00:15.1016127 (ExpandClause:  | FilterClause:  | SelectClause: id,state,environmentSettings)
5000 tasks retrieved in 00:00:17.0548145 (ExpandClause: stats | FilterClause:  | SelectClause: )

Sample complete, hit ENTER toocontinue...
```

<span data-ttu-id="78513-248">Как показано в hello промежутки времени, значительно может снизить время ответа на запрос, ограничивая свойства hello и количество элементов, возвращаемых в hello.</span><span class="sxs-lookup"><span data-stu-id="78513-248">As shown in hello elapsed times, you can greatly lower query response times by limiting hello properties and hello number of items that are returned.</span></span> <span data-ttu-id="78513-249">Это и другие примеры можно найти в hello [образцы azure пакета] [ github_samples] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="78513-249">You can find this and other sample projects in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span>

### <a name="batchmetrics-library-and-code-sample"></a><span data-ttu-id="78513-250">Библиотека BatchMetrics и пример кода</span><span class="sxs-lookup"><span data-stu-id="78513-250">BatchMetrics library and code sample</span></span>
<span data-ttu-id="78513-251">В дополнение к этому toohello EfficientListQueries приведенном выше примере можно найти hello [BatchMetrics] [ batch_metrics] проекта в hello [образцы azure пакета] [ github_samples] Репозиторий GitHub.</span><span class="sxs-lookup"><span data-stu-id="78513-251">In addition toohello EfficientListQueries code sample above, you can find hello [BatchMetrics][batch_metrics] project in hello [azure-batch-samples][github_samples] GitHub repository.</span></span> <span data-ttu-id="78513-252">проект Образец Hello BatchMetrics демонстрирует, как tooefficiently Мониторинг хода выполнения задания пакетной службы Azure, с помощью API пакета hello.</span><span class="sxs-lookup"><span data-stu-id="78513-252">hello BatchMetrics sample project demonstrates how tooefficiently monitor Azure Batch job progress using hello Batch API.</span></span>

<span data-ttu-id="78513-253">Hello [BatchMetrics] [ batch_metrics] пример включает проект библиотеки классов .NET, который можно включить в собственных проектах и простой командной строки программы tooexercise и демонстрируют использование hello hello Библиотека.</span><span class="sxs-lookup"><span data-stu-id="78513-253">hello [BatchMetrics][batch_metrics] sample includes a .NET class library project which you can incorporate into your own projects, and a simple command-line program tooexercise and demonstrate hello use of hello library.</span></span>

<span data-ttu-id="78513-254">Пример приложения Hello в рамках проекта hello демонстрирует hello следующие операции:</span><span class="sxs-lookup"><span data-stu-id="78513-254">hello sample application within hello project demonstrates hello following operations:</span></span>

1. <span data-ttu-id="78513-255">При выборе определенные атрибуты в свойствах только hello порядок toodownload необходимо</span><span class="sxs-lookup"><span data-stu-id="78513-255">Selecting specific attributes in order toodownload only hello properties you need</span></span>
2. <span data-ttu-id="78513-256">Фильтрация по времени перехода состояния в порядке toodownload изменяет только со времени последнего запроса hello</span><span class="sxs-lookup"><span data-stu-id="78513-256">Filtering on state transition times in order toodownload only changes since hello last query</span></span>

<span data-ttu-id="78513-257">Например следующий метод hello отображается в hello BatchMetrics библиотеки.</span><span class="sxs-lookup"><span data-stu-id="78513-257">For example, hello following method appears in hello BatchMetrics library.</span></span> <span data-ttu-id="78513-258">Возвращается значение, указывающее, что только hello ODATADetailLevel `id` и `state` для hello сущностей, которые получат нужно получить свойства.</span><span class="sxs-lookup"><span data-stu-id="78513-258">It returns an ODATADetailLevel that specifies that only hello `id` and `state` properties should be obtained for hello entities that are queried.</span></span> <span data-ttu-id="78513-259">Также указывает, что единственная сущность, состояние которого была изменена с момента hello указан `DateTime` должны возвращаться.</span><span class="sxs-lookup"><span data-stu-id="78513-259">It also specifies that only entities whose state has changed since hello specified `DateTime` parameter should be returned.</span></span>

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a><span data-ttu-id="78513-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78513-260">Next steps</span></span>
### <a name="parallel-node-tasks"></a><span data-ttu-id="78513-261">Параллельные задачи узла</span><span class="sxs-lookup"><span data-stu-id="78513-261">Parallel node tasks</span></span>
<span data-ttu-id="78513-262">[Максимально увеличить использование ресурсов вычислений пакета Azure с помощью узла параллельных задач](batch-parallel-node-tasks.md) является другой статьи tooBatch производительности приложения, связанных с.</span><span class="sxs-lookup"><span data-stu-id="78513-262">[Maximize Azure Batch compute resource usage with concurrent node tasks](batch-parallel-node-tasks.md) is another article related tooBatch application performance.</span></span> <span data-ttu-id="78513-263">Для эффективной обработки некоторых типов рабочих нагрузок можно применять параллельное выполнение задач на меньшем количестве более крупных вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="78513-263">Some types of workloads can benefit from executing parallel tasks on larger--but fewer--compute nodes.</span></span> <span data-ttu-id="78513-264">Извлечение hello [пример сценария](batch-parallel-node-tasks.md#example-scenario) hello статьи приведены сведения о такой сценарий.</span><span class="sxs-lookup"><span data-stu-id="78513-264">Check out hello [example scenario](batch-parallel-node-tasks.md#example-scenario) in hello article for details on such a scenario.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="78513-265">Форум по Пакетной службе</span><span class="sxs-lookup"><span data-stu-id="78513-265">Batch Forum</span></span>
<span data-ttu-id="78513-266">Hello [форум по пакетной Azure] [ forum] на сайте MSDN — лучшие поместите toodiscuss пакета и ответы на вопросы о службе hello.</span><span class="sxs-lookup"><span data-stu-id="78513-266">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="78513-267">Изучайте полезные «прикрепленные» сообщения и задавайте вопросы, возникающие во время сборки пакетных решений.</span><span class="sxs-lookup"><span data-stu-id="78513-267">Head on over for helpful "sticky" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_metrics]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchMetrics
[efficient_query_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/EfficientListQueries
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_samples]: https://github.com/Azure/azure-batch-samples
[odata]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[odata_ctor]: https://msdn.microsoft.com/library/azure/dn866178.aspx
[odata_expand]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.expandclause.aspx
[odata_filter]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.filterclause.aspx
[odata_select]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.selectclause.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[rest_list_certs]: https://msdn.microsoft.com/library/azure/dn820154.aspx
[rest_list_compute_nodes]: https://msdn.microsoft.com/library/azure/dn820159.aspx
[rest_list_job_schedules]: https://msdn.microsoft.com/library/azure/mt282174.aspx
[rest_list_jobprep_status]: https://msdn.microsoft.com/library/azure/mt282170.aspx
[rest_list_jobs]: https://msdn.microsoft.com/library/azure/dn820117.aspx
[rest_list_nodefiles]: https://msdn.microsoft.com/library/azure/dn820151.aspx
[rest_list_pools]: https://msdn.microsoft.com/library/azure/dn820101.aspx
[rest_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/mt282169.aspx
[rest_list_task_files]: https://msdn.microsoft.com/library/azure/dn820142.aspx
[rest_list_tasks]: https://msdn.microsoft.com/library/azure/dn820187.aspx

[rest_get_cert]: https://msdn.microsoft.com/library/azure/dn820176.aspx
[rest_get_job]: https://msdn.microsoft.com/library/azure/dn820106.aspx
[rest_get_node]: https://msdn.microsoft.com/library/azure/dn820168.aspx
[rest_get_pool]: https://msdn.microsoft.com/library/azure/dn820165.aspx
[rest_get_schedule]: https://msdn.microsoft.com/library/azure/mt282171.aspx
[rest_get_task]: https://msdn.microsoft.com/library/azure/dn820133.aspx

[net_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificate.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_schedule]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjobschedule.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx

[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job