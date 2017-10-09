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
# <a name="create-queries-toolist-batch-resources-efficiently"></a>Эффективно создавать запросы toolist пакета ресурсов

Здесь вы узнаете, как tooincrease производительность приложения пакетной службы Azure, уменьшая hello объем данных, возвращаемых службой hello при запросе заданий, задач и вычислительных узлов с hello [пакета .NET] [ api_net] библиотеки.

Практически все приложения пакета должны tooperform некоторые типы операций мониторинга или другие запросы пакетная служба hello, часто через регулярные интервалы. Например, toodetermine являются ли все задачи в очереди, оставшихся в задании должен получить данные для каждой задачи в задании hello. состояние hello toodetermine узлов в пул, необходимо получить данные на каждом узле в пуле hello. В этой статье объясняется, как tooexecute такие запросы в hello наиболее эффективным способом.

> [!NOTE]
> Hello пакетная служба поддерживает специальные API распространенный сценарий hello подсчет задач в задании. Вместо этих запрос списка, можно вызвать hello [получить количество задач] [ rest_get_task_counts] операции. Эта операция указывает количество задач, ожидающих выполнения, запущенных, завершенных, успешно или неудачно выполненных задач. Это операция эффективнее запроса списка. Дополнительные сведения см. в статье [Подсчет задач по состоянию для мониторинга хода выполнения задания (предварительная версия)](batch-get-task-counts.md). 
>
> Hello получить количество задач операция недоступна в версии пакета обновления более ранней, чем 2017 г-06-01.5.1. Если вы используете старую версию службы hello, затем используйте задачи toocount список запросов в задании.
>
> 

## <a name="meet-hello-detaillevel"></a>Соответствует hello DetailLevel
В рабочей среде пакета приложения пронумеровать сущности, такие как задания, задач и вычислительных узлов можно hello тысяч. При запросе сведения о таких ресурсах потенциально большой объем данных должен» cross передачи hello» из службы tooyour hello пакета приложения на каждый запрос. Ограничивая hello число элементов и тип данных, возвращаемых запросом, может увеличить hello ускорения обработки запросов и поэтому hello производительности приложения.

Это [пакета .NET] [ api_net] списки фрагментов кода API *каждого* задач, связанных с заданием, вместе с *все* hello свойств каждого задача.

```csharp
// Get a collection of all of hello tasks and all of their properties for job-001
IPagedEnumerable<CloudTask> allTasks =
    batchClient.JobOperations.ListTasks("job-001");
```

Запрос списка намного более эффективным, тем не менее, можно выполнить путем применения запроса tooyour «уровень детализации». Это делается путем указания [ODATADetailLevel] [ odata] объекта toohello [JobOperations.ListTasks] [ net_list_tasks] метод. Этот фрагмент возвращает только идентификатор hello, командной строки, вычислений свойства узла и сведения о завершенных задач:

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

В этом примере сценария, если существуют тысячи задачи в задании hello hello результаты из второго запроса hello обычно будут возвращены первыми намного быстрее, чем hello. Дополнительные сведения об использовании ODATADetailLevel при перечислении элементов с помощью пакета .NET API hello включено [ниже](#efficient-querying-in-batch-net).

> [!IMPORTANT]
> Настоятельно рекомендуется, чтобы вы *всегда* введите список .NET API tooyour ODATADetailLevel объекта вызывает tooensure Максимальная эффективность и производительность приложения. Если задать уровень детализации, может помочь toolower пакетной службы времени отклика, повысить эффективность использования сети и свести к минимуму использование памяти клиентскими приложениями.
> 
> 

## <a name="filter-select-and-expand"></a>Фильтрация, выборка и развертывание
Hello [пакета .NET] [ api_net] и [REST пакетной] [ api_rest] API обеспечивают возможность tooreduce hello обоих hello число элементов, которые возвращаются в виде списка а также объем сведений, возвращаемых для каждой hello. Для этого в запросе необходимо указать строки **фильтрации**, **выборки** и **развертывания**.

### <a name="filter"></a>Фильтр
Строка Hello фильтра — это выражение, уменьшает количество элементов, возвращаемых в hello. Например список только hello выполняемые задачи для задания или список только вычислительных узлов, которые готовы toorun задачи.

* Строка Hello фильтра состоит из одного или нескольких выражений, с помощью выражения, которая состоит из имени свойства, оператор и значение. Hello свойства, которые могут быть указаны являются tooeach определенного типа сущности, который вы выполняете запрос, hello операторы, которые поддерживаются для каждого свойства.
* Несколько выражений, которые могут быть объединены с помощью логических операторов hello `and` и `or`.
* В этом примере фильтрация списков строк только под управлением hello «визуализации» задачи: `(state eq 'running') and startswith(id, 'renderTask')`.

### <a name="select"></a>Выберите пункт
Выберите строку Hello ограничивает hello значения свойств, которые возвращаются для каждого элемента. Укажите список имен свойств и для элементов hello в результатах запроса hello возвращаются только те значения свойства.

* Выберите строку Hello состоит из разделенных запятыми список имен свойств. Можно указать любую hello свойств для типа сущности hello, выполнении запроса.
* В этом примере строка выборки указывает, что для каждой задачи необходимо вернуть значения только трех свойств: `id, state, stateTransitionTime`.

### <a name="expand"></a>Разверните
Hello разверните строку уменьшает число hello вызовы API, необходимые tooobtain определенные сведения. При использовании строки развертывания дополнительные сведения о каждом элементе можно получить с помощью одного вызова API. Вместо того чтобы первого получения hello список сущностей, а затем запросом сведений для каждого элемента в списке hello, используйте строку развернуть tooobtain hello одинаковые данные в одном вызове API. Чем меньше вызовов API, тем выше производительность.

* Аналогичные toohello выберите строку, hello разверните элементы управления строки ли определенные данные включаются в список результатов запроса.
* Hello разверните строку поддерживается только в том случае, когда он используется в список заданий, расписаний заданий, задач и пулы. В настоящее время они поддерживают только статистические данные.
* Если необходимы все свойства и выберите Строка не указана, hello разверните строку *должен* быть используется tooget статистические данные. Если строка select — используется tooobtain подмножество свойств, затем `stats` может задаваться в строке выберите hello и hello разверните строку не требуется toobe указано.
* В этом примере разверните строка указывает, что статистические данные должны быть возвращены для каждого элемента в списке hello: `stats`.

> [!NOTE]
> При создании любого hello три запроса строковые типы (фильтрации, выберите и разверните), необходимо убедиться, имена свойств hello и case совпадали с их аналогами элемент интерфейса API REST. Например, при работе с hello .NET [CloudTask](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask) , необходимо указать **состояние** вместо **состояние**, даже если hello свойство .NET — [ CloudTask.State](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.state). В разделе hello таблицы ниже для сопоставления свойств между hello .NET и API-интерфейсов REST.
> 
> 

### <a name="rules-for-filter-select-and-expand-strings"></a>Правила строк фильтрации, выборки и развертывания
* Имена свойств в фильтре, выберите и разверните строк должны отображаться как в hello [REST пакетной] [ api_rest] API — даже при использовании [пакета .NET] [ api_net] или одного из других пакета SDK для hello.
* Имена всех свойств чувствительны к регистру, но для значений свойств регистр значения не имеет.
* Строки даты и времени могут иметь один из двух форматов и должны начинаться с `DateTime`.
  
  * Пример формата W3C-DTF: `creationTime gt DateTime'2011-05-08T08:49:37Z'`
  * Пример формата RFC 1123: `creationTime gt DateTime'Sun, 08 May 2011 08:49:37 GMT'`
* Строки с логическими выражениями должны иметь значение `true` или `false`.
* Если задано недопустимое свойство или оператор, отобразится ошибка `400 (Bad Request)` .

## <a name="efficient-querying-in-batch-net"></a>Эффективное выполнение запросов в пакетной службе для .NET
В рамках hello [пакета .NET] [ api_net] API, hello [ODATADetailLevel] [ odata] класс используется для указания фильтра, выберите и разверните строк toolist операции. Hello ODataDetailLevel класс имеет три строку открытого свойства, которые могут быть определены в конструкторе hello, или задать непосредственно hello объекта. Затем передается hello ODataDetailLevel объект как toohello параметр различные операции списка таких как [ListPools][net_list_pools], [ListJobs][net_list_jobs], и [ListTasks][net_list_tasks].

* [ODATADetailLevel][odata].[ FilterClause][odata_filter]: максимальное число элементов, возвращаемых hello.
* [ODATADetailLevel][odata].[SelectClause][odata_select]: определяет, значения каких свойств необходимо вернуть для каждого элемента.
* [ODATADetailLevel][odata].[ExpandClause][odata_expand]: извлекает данные по всем элементам за один вызов API вместо того, чтобы выполнять отдельные вызовы для каждого элемента.

Hello следующий фрагмент кода hello пакета .NET API tooefficiently запроса hello пакета служба используется для статистики hello определенного набора пулов. В этом сценарии hello пакета пользователем тестовой и рабочей группы. Hello теста пул идентификаторов имеют префикс «test» и hello Производственный кластер идентификаторы имеют префикс «prod». Во фрагменте hello *myBatchClient* — это правильно инициализированный экземпляр hello [BatchClient](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient) класса.

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
> Экземпляр [ODATADetailLevel] [ odata] , настроенный с помощью Select и Expand предложений также можно передать методы Get tooappropriate, такие как [PoolOperations.GetPool](https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getpool.aspx) , toolimit hello объем возвращаемых данных.
> 
> 

## <a name="batch-rest-toonet-api-mappings"></a>Сопоставления REST too.NET API пакета
Имена и регистр свойств в строках фильтрации, выборки и развертывания *должны* полностью соответствовать аналогичным элементам в REST API. Hello ниже приведены сопоставления между hello .NET и API-интерфейса REST эквивалентами.

### <a name="mappings-for-filter-strings"></a>Сопоставления для строк фильтрации
* **Список методов .NET**: каждый из методов .NET API hello в этом столбце принимает [ODATADetailLevel] [ odata] объект в качестве параметра.
* **Список запросов REST**: каждый API REST страницы связанного tooin этот столбец содержит таблицу, которая задает свойства hello и операции, допустимых в *фильтра* строки. Эти имена свойств и операции будут использоваться при создании строки [ODATADetailLevel.FilterClause][odata_filter].

| Методы списка .NET | Запросы списка REST |
| --- | --- |
| [CertificateOperations.ListCertificates][net_list_certs] |[Список сертификатов hello в учетной записи][rest_list_certs] |
| [CloudTask.ListNodeFiles][net_list_task_files] |[Список файлов hello, связанного с задачей][rest_list_task_files] |
| [JobOperations.ListJobPreparationAndReleaseTaskStatus][net_list_jobprep_status] |[Отображение состояния hello hello подготовки задания и задания выпуска задачи для задания][rest_list_jobprep_status] |
| [JobOperations.ListJobs][net_list_jobs] |[Перечисление заданий hello в учетной записи][rest_list_jobs] |
| [JobOperations.ListNodeFiles][net_list_nodefiles] |[Список файлов hello на узле][rest_list_nodefiles] |
| [JobOperations.ListTasks][net_list_tasks] |[Список задач hello, связанных с заданием][rest_list_tasks] |
| [JobScheduleOperations.ListJobSchedules][net_list_job_schedules] |[Список расписаний заданий hello в учетной записи][rest_list_job_schedules] |
| [JobScheduleOperations.ListJobs][net_list_schedule_jobs] |[Список заданий hello, связанных с расписания задания][rest_list_schedule_jobs] |
| [PoolOperations.ListComputeNodes][net_list_compute_nodes] |[Список hello вычислительных узлов в пуле][rest_list_compute_nodes] |
| [PoolOperations.ListPools][net_list_pools] |[Список пулов hello в учетной записи][rest_list_pools] |

### <a name="mappings-for-select-strings"></a>Сопоставления для строк выборки
* **Типы пакетной службы для .NET**— типы API пакетной службы для .NET.
* **Сущности REST API**: каждая страница в этот столбец содержит одну или несколько таблиц, в которых перечислены имена свойств hello REST API для типа hello. Эти имена свойств используются при создании строк *выборки* . Они также будут использоваться при создании строки [ODATADetailLevel.SelectClause][odata_select].

| Типы пакетной службы для .NET | Сущности REST API |
| --- | --- |
| [Certificate][net_cert] |[Получение информации о сертификате][rest_get_cert] |
| [CloudJob][net_job] |[Получение информации о задании][rest_get_job] |
| [CloudJobSchedule][net_schedule] |[Получение информации о расписании задания][rest_get_schedule] |
| [ComputeNode][net_node] |[Получение информации об узле][rest_get_node] |
| [CloudPool][net_pool] |[Получение информации о пуле][rest_get_pool] |
| [CloudTask][net_task] |[Получение информации о задаче][rest_get_task] |

## <a name="example-construct-a-filter-string"></a>Пример. Создание строки фильтрации
При построении строку фильтра для [ODATADetailLevel.FilterClause][odata_filter], обратитесь к таблице hello выше в разделе «Сопоставлений для фильтрации строк» toofind hello API-интерфейса REST страницы документации, которая соответствует операции вывода списка toohello обратиться в tooperform. В первой таблице многострочные hello на этой странице можно найти hello фильтруемых свойств и их поддерживаемые операторы. При желании tooretrieve все задачи, код выхода был ненулевое значение, например, это строк на [список hello задач, связанных с заданием] [ rest_list_tasks] задает строку применимым свойством hello и допустимые операторы:

| Свойство | Разрешенные операции | Тип |
|:--- |:--- |:--- |
| `executionInfo/exitCode` |`eq, ge, gt, le , lt` |`Int` |

Таким образом будет hello строку фильтра для перечисления всех задач с ненулевой код выхода:

`(executionInfo/exitCode lt 0) or (executionInfo/exitCode gt 0)`

## <a name="example-construct-a-select-string"></a>Пример. Создание строки выборки
tooconstruct [ODATADetailLevel.SelectClause][odata_select], обратитесь к таблице hello выше в разделе «Сопоставлений для выбора строк» и перейти страницу toohello REST API, соответствующий toohello тип сущности, которые списка. В первой таблице многострочные hello на этой странице можно найти доступный для выбора свойств hello и их поддерживаемые операторы. Желанию tooretrieve только идентификатор hello и командную строку для каждой задачи в списке, например, можно найти эти строки в таблице применимо hello на [получить сведения о задаче][rest_get_task]:

| Свойство | Тип | Примечания |
|:--- |:--- |:--- |
| `id` |`String` |`hello ID of hello task.` |
| `commandLine` |`String` |`hello command line of hello task.` |

Выберите строку Hello для включения только идентификатор hello и командной строки с каждой из перечисленных задач будет следующим:

`id, commandLine`

## <a name="code-samples"></a>Примеры кода
### <a name="efficient-list-queries-code-sample"></a>Пример кода с эффективными запросами списков
Извлечение hello [EfficientListQueries] [ efficient_query_sample] примера проекта на GitHub toosee эффективность список запросов может повлиять на производительность приложения. Это консольное приложение C# создается и добавляется большое количество задач tooa задания. Затем, выполняются несколько вызовов toohello [JobOperations.ListTasks] [ net_list_tasks] метод и передает [ODATADetailLevel] [ odata] объекты, которые являются настроить другое свойство значения toovary hello объем возвращаемых toobe данных. Она дает примерно toohello следующие выходные данные:

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

Как показано в hello промежутки времени, значительно может снизить время ответа на запрос, ограничивая свойства hello и количество элементов, возвращаемых в hello. Это и другие примеры можно найти в hello [образцы azure пакета] [ github_samples] репозитория в GitHub.

### <a name="batchmetrics-library-and-code-sample"></a>Библиотека BatchMetrics и пример кода
В дополнение к этому toohello EfficientListQueries приведенном выше примере можно найти hello [BatchMetrics] [ batch_metrics] проекта в hello [образцы azure пакета] [ github_samples] Репозиторий GitHub. проект Образец Hello BatchMetrics демонстрирует, как tooefficiently Мониторинг хода выполнения задания пакетной службы Azure, с помощью API пакета hello.

Hello [BatchMetrics] [ batch_metrics] пример включает проект библиотеки классов .NET, который можно включить в собственных проектах и простой командной строки программы tooexercise и демонстрируют использование hello hello Библиотека.

Пример приложения Hello в рамках проекта hello демонстрирует hello следующие операции:

1. При выборе определенные атрибуты в свойствах только hello порядок toodownload необходимо
2. Фильтрация по времени перехода состояния в порядке toodownload изменяет только со времени последнего запроса hello

Например следующий метод hello отображается в hello BatchMetrics библиотеки. Возвращается значение, указывающее, что только hello ODATADetailLevel `id` и `state` для hello сущностей, которые получат нужно получить свойства. Также указывает, что единственная сущность, состояние которого была изменена с момента hello указан `DateTime` должны возвращаться.

```csharp
internal static ODATADetailLevel OnlyChangedAfter(DateTime time)
{
    return new ODATADetailLevel(
        selectClause: "id, state",
        filterClause: string.Format("stateTransitionTime gt DateTime'{0:o}'", time)
    );
}
```

## <a name="next-steps"></a>Дальнейшие действия
### <a name="parallel-node-tasks"></a>Параллельные задачи узла
[Максимально увеличить использование ресурсов вычислений пакета Azure с помощью узла параллельных задач](batch-parallel-node-tasks.md) является другой статьи tooBatch производительности приложения, связанных с. Для эффективной обработки некоторых типов рабочих нагрузок можно применять параллельное выполнение задач на меньшем количестве более крупных вычислительных узлов. Извлечение hello [пример сценария](batch-parallel-node-tasks.md#example-scenario) hello статьи приведены сведения о такой сценарий.

### <a name="batch-forum"></a>Форум по Пакетной службе
Hello [форум по пакетной Azure] [ forum] на сайте MSDN — лучшие поместите toodiscuss пакета и ответы на вопросы о службе hello. Изучайте полезные «прикрепленные» сообщения и задавайте вопросы, возникающие во время сборки пакетных решений.

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