---
title: "aaaTutorial - использование клиентской библиотеки hello пакетной службы Azure для Node.js | Документы Microsoft"
description: "Изучите основные понятия hello пакетной службы Azure и создайте простое решение, с помощью Node.js."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Приступая к работе с пакетом SDK для пакетной службы для Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Основы hello построения пакета клиента в Node.js с помощью [Node.js пакета Azure SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Мы определим ключевые аспекты приложения пакетной службы, а затем настроим его с помощью клиента Node.js.  

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже работали с Node.js и знаете, как работать в Linux. Он также предполагается, что при установке учетная запись Azure с доступом права toocreate пакета службы и службы хранилища.

Мы рекомендуем чтения [Технический обзор пакетной Azure](batch-technical-overview.md) до перехода hello шаги, описанные в этой статье.

## <a name="hello-tutorial-scenario"></a>сценарий учебника Hello
Рассмотрим сценарий рабочего процесса пакета hello. У нас есть простой сценарий, написанный на Python, который загружает все csv файлов из контейнер службы хранилища больших двоичных объектов Azure и преобразует их tooJSON. tooprocess несколько учетную запись хранилища, контейнеры параллельно, разворачиваются hello скрипт как задание пакетной службы Azure.

## <a name="azure-batch-architecture"></a>Архитектура пакетной службы Azure
Hello следующая диаграмма изображает как можно масштабировать hello сценарий Python, с помощью пакетной службы Azure и клиент Node.js.

![Сценарий пакетной службы Azure](./media/batch-nodejs-get-started/BatchScenario.png)

Клиент node.js Hello развертывает пакетного задания с задача «Подготовка» (подробно рассматривается позже) и набор задач, в зависимости от hello количество контейнеров в учетной записи хранения hello. Hello скрипты можно загрузить из репозитория github hello.

* [Клиент Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Скрипты оболочки для задач подготовки](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Процессор tooJSON csv Python](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> Клиент Node.js Hello в ссылке hello указано не содержит развернут как приложение Azure функция toobe конкретного кода. Можно ссылаться toohello ссылкам для инструкции toocreate один.
> - [Создание приложения-функции](../azure-functions/functions-create-first-azure-function.md)
> - [Триггер таймера](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Создание приложения hello

Теперь давайте Пройдите hello шаг за шагом в построении hello Node.js клиента:

### <a name="step-1-install-azure-batch-sdk"></a>Шаг 1. Установка пакета SDK для пакетной службы Azure

Можно установить пакет Azure SDK для Node.js с помощью команды install npm hello.

`npm install azure-batch`

Эта команда устанавливает последнюю версию hello узла пакета azure SDK.

>[!Tip]
> В приложении функции Azure, вы можете перейти слишком npm hello toorun вкладку «Kudu консоли» hello Azure функции параметры установки команды. В этом вариантов tooinstall Azure пакета SDK для Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Шаг 2. Создание учетной записи пакетной службы Azure

Вы можете создать на hello [портал Azure](batch-account-create-portal.md) или из командной строки ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).

Ниже приведены команды hello toocreate, один через Azure CLI.

Создание группы ресурсов, пропустите этот шаг, если она уже есть место toocreate hello пакетной учетной записи:

`az group create -n "<resource-group-name>" -l "<location>"`

Создайте учетную запись пакетной службы Azure.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Каждая учетная запись пакетной службы имеет соответствующие ключи доступа. Эти разделы находятся необходимые toocreate дополнительные ресурсы в учетной записи пакетной службы Azure. Рекомендуется для рабочей среды является toostore toouse хранилище ключей Azure, эти ключи. Затем можно создать службу участника для приложения hello. С помощью этого приложения hello участника службы, можно создать ключи tooaccess токена OAuth из хранилища ключей hello.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Скопируйте и сохраните toobe hello ключа, используемые в последующих шагах hello.

### <a name="step-3-create-an-azure-batch-service-client"></a>Шаг 3. Создание клиента пакетной службы Azure
Следующий фрагмент кода сначала импортирует модуль Node.js hello azure пакета, а затем создает клиент пакетной службы. Требуется toofirst создайте объект SharedKeyCredentials и ключ учетной записи пакетной hello, скопированные из предыдущего шага hello.

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

Hello Azure URI пакета можно найти в hello игнорировались hello портал Azure. Он имеет формат hello:

`https://accountname.location.batch.azure.com`

См. снимок экрана toohello:

![URI пакетной службы Azure](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Шаг 4. Создание пула пакетной службы Azure
Пул пакетной службы Azure состоит из нескольких виртуальных машин (также известных как узлы пакетной службы). Служба Azure Batch развертывает hello задачи на этих узлах и управляет ими. Можно определить следующие параметры конфигурации для пула hello.

* тип образа виртуальной машины;
* размер узлов виртуальной машины;
* число узлов виртуальной машины.

> [!Tip]
> размер Hello и количества узлов виртуальных машин во многом зависят от hello число задач, которые требуется toorun в параллельно, а также саму задачу hello. Корпорация Майкрософт рекомендует тестирование toodetermine hello идеальное число и размер.
>
>

Hello следующий фрагмент кода создает hello объекты параметров конфигурации.

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> Hello список образов виртуальных Машин Linux, доступны для пакетной службы Azure и их идентификаторы SKU см. в разделе [список образов виртуальных машин](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

После определения конфигурации пула hello, можно создать пул hello пакетной службы Azure. Hello пула Batch, команда создает узлы виртуальной машины Azure и подготовить их tooexecute задачи готовности tooreceive toobe. Каждый пул должен иметь уникальный идентификатор, чтобы на него можно было ссылаться на последующих шагах.

Следующий фрагмент кода Hello создает пул пакетной службы Azure.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Можно проверить состояние hello пула hello создан и убедитесь, что состояние hello в «активный», перед продолжением отправки пула toothat задания.

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

Ниже приведен пример результирующий объект, возвращенный функцией pool.get hello.

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a>Шаг 4. Отправка задания пакетной службы Azure
Задание пакетной службы Azure представляет собой логическую группу схожих задач. В нашем случае это «TooJSON csv процесса». В нем каждая задача может обрабатывать CSV-файлы, которые присутствуют в каждом контейнере службы хранилища Azure.

Эти задачи будут выполняться параллельно и развернуть на нескольких узлах под управлением hello пакетной службы Azure.

> [!Tip]
> Можно использовать hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) свойство toospecify максимальное число задач, которые могут выполняться параллельно на одном узле.
>
>

#### <a name="preparation-task"></a>Задача подготовки

Hello узлов виртуальных Машин, созданных являются пустой Ubuntu узлами. Часто требуется tooinstall набор программ, в качестве необходимых компонентов.
Как правило для узлов Linux может иметь сценарий, который устанавливает компоненты hello перед выполнения фактических задач hello. Однако это может быть любой программируемый исполняемый файл.
Hello [оболочки сценарий](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) в этом примере устанавливает Python pip и hello пакет SDK хранилища Azure для Python.

Можно загрузить скрипт hello на учетную запись хранилища Azure и создать сценарий hello tooaccess универсальный код Ресурса SAS. Также этот процесс можно автоматизировать с помощью hello пакет SDK для Node.js хранилища Azure.

> [!Tip]
> Задача «Подготовка» для задания выполняется только на узлах виртуальных Машин hello целей toorun hello конкретной задачи. Если требуется toobe необходимые компоненты установлены на всех узлах, независимо от hello задач, которые выполняются на нем можно использовать hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) свойства во время добавления в пул. Можно использовать hello после определения задачи подготовки для ссылки.
>
>

Задача «Подготовка» задается во время передачи hello Azure пакетного задания. Параметры конфигурации задачи подготовки Здравствуйте, следующие:

* **Идентификатор**: Уникальный идентификатор для задачи подготовки hello
* **Командная строка**: исполняемый файл задачи hello tooexecute командной строки
* **resourceFiles**: массив объектов, предоставляющих подробные сведения о файлах требуется загрузить для этой задачи toorun toobe.  Ниже приведены его параметры.
    - blobSource: hello SAS URI файла hello
    - filePath: toodownload локальный путь и сохраните файл hello
    - fileMode: применим только для узлов Linux. fileMode имеет восьмеричный формат и значение по умолчанию 0770.
* **waitForSuccess**: Если set tootrue, задачу hello не выполняется при сбое задачи подготовки
* **runElevated**: задать для него tootrue повышенные привилегии в случае необходимости toorun задачу hello.

Следующий фрагмент кода показывает образец hello подготовки задачи скрипта конфигурации:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Если не toobe необходимые компоненты установлены для вашей toorun задачи, можно пропустить задачи подготовки hello. Следующий код создает задание с отображаемым именем process csv files.

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Шаг 5. Отправка задач пакетной службы Azure для задания

Теперь, когда задание преобразования CSV-файлов создано, можно создать задачи для него. Предположим, что у нас есть четыре контейнеров, у нас есть четыре задачи toocreate, один для каждого контейнера.

Если взглянуть на hello [сценарий Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), он принимает два параметра:

* Имя контейнера: hello файлы toodownload контейнера хранилища из
* pattern: необязательный параметр шаблона имени файла.

Предположим, что у нас есть четыре контейнеры «con1», «con2», «con3», «con4» ниже показан отправкой на задачи toohello Azure пакетного задания «процесса csv» созданную ранее.

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

Hello код добавляет пул toohello несколько задач. И каждая из задач hello выполняется на узле в пуле hello создания виртуальных машин. Если hello число задач превышает hello число виртуальных машин в свойстве maxTasksPerNode пула или hello, задачи hello Подождите, пока узел станет доступным. Это задание оркестрации пакетная служба Azure обрабатывает автоматически.

портал Hello содержатся подробные представления для задач hello и состояний задания. Можно также использовать список hello и функции получения в hello узла Azure SDK. Подробные сведения приведены в документации hello [ссылку](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Дальнейшие действия

- Просмотрите hello [возможности пакетной обработки Обзор Azure](batch-api-basics.md) статьи, которая рекомендуется, если вы новую службу toohello.
- . В разделе hello [ссылку пакета Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API пакета.

