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
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="ec240-103">Приступая к работе с пакетом SDK для пакетной службы для Node.js</span><span class="sxs-lookup"><span data-stu-id="ec240-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec240-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ec240-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="ec240-105">Python</span><span class="sxs-lookup"><span data-stu-id="ec240-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="ec240-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ec240-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="ec240-107">Основы hello построения пакета клиента в Node.js с помощью [Node.js пакета Azure SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="ec240-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="ec240-108">Мы определим ключевые аспекты приложения пакетной службы, а затем настроим его с помощью клиента Node.js.</span><span class="sxs-lookup"><span data-stu-id="ec240-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ec240-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ec240-109">Prerequisites</span></span>
<span data-ttu-id="ec240-110">В этой статье предполагается, что вы уже работали с Node.js и знаете, как работать в Linux.</span><span class="sxs-lookup"><span data-stu-id="ec240-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="ec240-111">Он также предполагается, что при установке учетная запись Azure с доступом права toocreate пакета службы и службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec240-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="ec240-112">Мы рекомендуем чтения [Технический обзор пакетной Azure](batch-technical-overview.md) до перехода hello шаги, описанные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ec240-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="ec240-113">сценарий учебника Hello</span><span class="sxs-lookup"><span data-stu-id="ec240-113">hello tutorial scenario</span></span>
<span data-ttu-id="ec240-114">Рассмотрим сценарий рабочего процесса пакета hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="ec240-115">У нас есть простой сценарий, написанный на Python, который загружает все csv файлов из контейнер службы хранилища больших двоичных объектов Azure и преобразует их tooJSON.</span><span class="sxs-lookup"><span data-stu-id="ec240-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="ec240-116">tooprocess несколько учетную запись хранилища, контейнеры параллельно, разворачиваются hello скрипт как задание пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="ec240-117">Архитектура пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ec240-117">Azure Batch Architecture</span></span>
<span data-ttu-id="ec240-118">Hello следующая диаграмма изображает как можно масштабировать hello сценарий Python, с помощью пакетной службы Azure и клиент Node.js.</span><span class="sxs-lookup"><span data-stu-id="ec240-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Сценарий пакетной службы Azure](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="ec240-120">Клиент node.js Hello развертывает пакетного задания с задача «Подготовка» (подробно рассматривается позже) и набор задач, в зависимости от hello количество контейнеров в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="ec240-121">Hello скрипты можно загрузить из репозитория github hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="ec240-122">Клиент Node.js</span><span class="sxs-lookup"><span data-stu-id="ec240-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="ec240-123">Скрипты оболочки для задач подготовки</span><span class="sxs-lookup"><span data-stu-id="ec240-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="ec240-124">Процессор tooJSON csv Python</span><span class="sxs-lookup"><span data-stu-id="ec240-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="ec240-125">Клиент Node.js Hello в ссылке hello указано не содержит развернут как приложение Azure функция toobe конкретного кода.</span><span class="sxs-lookup"><span data-stu-id="ec240-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="ec240-126">Можно ссылаться toohello ссылкам для инструкции toocreate один.</span><span class="sxs-lookup"><span data-stu-id="ec240-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="ec240-127">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="ec240-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="ec240-128">Триггер таймера</span><span class="sxs-lookup"><span data-stu-id="ec240-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="ec240-129">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="ec240-129">Build hello application</span></span>

<span data-ttu-id="ec240-130">Теперь давайте Пройдите hello шаг за шагом в построении hello Node.js клиента:</span><span class="sxs-lookup"><span data-stu-id="ec240-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="ec240-131">Шаг 1. Установка пакета SDK для пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ec240-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="ec240-132">Можно установить пакет Azure SDK для Node.js с помощью команды install npm hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="ec240-133">Эта команда устанавливает последнюю версию hello узла пакета azure SDK.</span><span class="sxs-lookup"><span data-stu-id="ec240-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="ec240-134">В приложении функции Azure, вы можете перейти слишком npm hello toorun вкладку «Kudu консоли» hello Azure функции параметры установки команды.</span><span class="sxs-lookup"><span data-stu-id="ec240-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="ec240-135">В этом вариантов tooinstall Azure пакета SDK для Node.js.</span><span class="sxs-lookup"><span data-stu-id="ec240-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="ec240-136">Шаг 2. Создание учетной записи пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ec240-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="ec240-137">Вы можете создать на hello [портал Azure](batch-account-create-portal.md) или из командной строки ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="ec240-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="ec240-138">Ниже приведены команды hello toocreate, один через Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ec240-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="ec240-139">Создание группы ресурсов, пропустите этот шаг, если она уже есть место toocreate hello пакетной учетной записи:</span><span class="sxs-lookup"><span data-stu-id="ec240-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="ec240-140">Создайте учетную запись пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="ec240-141">Каждая учетная запись пакетной службы имеет соответствующие ключи доступа.</span><span class="sxs-lookup"><span data-stu-id="ec240-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="ec240-142">Эти разделы находятся необходимые toocreate дополнительные ресурсы в учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="ec240-143">Рекомендуется для рабочей среды является toostore toouse хранилище ключей Azure, эти ключи.</span><span class="sxs-lookup"><span data-stu-id="ec240-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="ec240-144">Затем можно создать службу участника для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="ec240-145">С помощью этого приложения hello участника службы, можно создать ключи tooaccess токена OAuth из хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="ec240-146">Скопируйте и сохраните toobe hello ключа, используемые в последующих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="ec240-147">Шаг 3. Создание клиента пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ec240-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="ec240-148">Следующий фрагмент кода сначала импортирует модуль Node.js hello azure пакета, а затем создает клиент пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ec240-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="ec240-149">Требуется toofirst создайте объект SharedKeyCredentials и ключ учетной записи пакетной hello, скопированные из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

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

<span data-ttu-id="ec240-150">Hello Azure URI пакета можно найти в hello игнорировались hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="ec240-151">Он имеет формат hello:</span><span class="sxs-lookup"><span data-stu-id="ec240-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="ec240-152">См. снимок экрана toohello:</span><span class="sxs-lookup"><span data-stu-id="ec240-152">Refer toohello screenshot:</span></span>

![URI пакетной службы Azure](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="ec240-154">Шаг 4. Создание пула пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ec240-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="ec240-155">Пул пакетной службы Azure состоит из нескольких виртуальных машин (также известных как узлы пакетной службы).</span><span class="sxs-lookup"><span data-stu-id="ec240-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="ec240-156">Служба Azure Batch развертывает hello задачи на этих узлах и управляет ими.</span><span class="sxs-lookup"><span data-stu-id="ec240-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="ec240-157">Можно определить следующие параметры конфигурации для пула hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="ec240-158">тип образа виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="ec240-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="ec240-159">размер узлов виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="ec240-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="ec240-160">число узлов виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ec240-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="ec240-161">размер Hello и количества узлов виртуальных машин во многом зависят от hello число задач, которые требуется toorun в параллельно, а также саму задачу hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="ec240-162">Корпорация Майкрософт рекомендует тестирование toodetermine hello идеальное число и размер.</span><span class="sxs-lookup"><span data-stu-id="ec240-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="ec240-163">Hello следующий фрагмент кода создает hello объекты параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ec240-163">hello following code snippet creates hello configuration parameter objects.</span></span>

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
> <span data-ttu-id="ec240-164">Hello список образов виртуальных Машин Linux, доступны для пакетной службы Azure и их идентификаторы SKU см. в разделе [список образов виртуальных машин](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="ec240-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="ec240-165">После определения конфигурации пула hello, можно создать пул hello пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="ec240-166">Hello пула Batch, команда создает узлы виртуальной машины Azure и подготовить их tooexecute задачи готовности tooreceive toobe.</span><span class="sxs-lookup"><span data-stu-id="ec240-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="ec240-167">Каждый пул должен иметь уникальный идентификатор, чтобы на него можно было ссылаться на последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="ec240-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="ec240-168">Следующий фрагмент кода Hello создает пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="ec240-169">Можно проверить состояние hello пула hello создан и убедитесь, что состояние hello в «активный», перед продолжением отправки пула toothat задания.</span><span class="sxs-lookup"><span data-stu-id="ec240-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

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

<span data-ttu-id="ec240-170">Ниже приведен пример результирующий объект, возвращенный функцией pool.get hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-170">Following is a sample result object returned by hello pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="ec240-171">Шаг 4. Отправка задания пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ec240-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="ec240-172">Задание пакетной службы Azure представляет собой логическую группу схожих задач.</span><span class="sxs-lookup"><span data-stu-id="ec240-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="ec240-173">В нашем случае это «TooJSON csv процесса».</span><span class="sxs-lookup"><span data-stu-id="ec240-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="ec240-174">В нем каждая задача может обрабатывать CSV-файлы, которые присутствуют в каждом контейнере службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="ec240-175">Эти задачи будут выполняться параллельно и развернуть на нескольких узлах под управлением hello пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="ec240-176">Можно использовать hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) свойство toospecify максимальное число задач, которые могут выполняться параллельно на одном узле.</span><span class="sxs-lookup"><span data-stu-id="ec240-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="ec240-177">Задача подготовки</span><span class="sxs-lookup"><span data-stu-id="ec240-177">Preparation task</span></span>

<span data-ttu-id="ec240-178">Hello узлов виртуальных Машин, созданных являются пустой Ubuntu узлами.</span><span class="sxs-lookup"><span data-stu-id="ec240-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="ec240-179">Часто требуется tooinstall набор программ, в качестве необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="ec240-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="ec240-180">Как правило для узлов Linux может иметь сценарий, который устанавливает компоненты hello перед выполнения фактических задач hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="ec240-181">Однако это может быть любой программируемый исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="ec240-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="ec240-182">Hello [оболочки сценарий](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) в этом примере устанавливает Python pip и hello пакет SDK хранилища Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="ec240-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="ec240-183">Можно загрузить скрипт hello на учетную запись хранилища Azure и создать сценарий hello tooaccess универсальный код Ресурса SAS.</span><span class="sxs-lookup"><span data-stu-id="ec240-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="ec240-184">Также этот процесс можно автоматизировать с помощью hello пакет SDK для Node.js хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ec240-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="ec240-185">Задача «Подготовка» для задания выполняется только на узлах виртуальных Машин hello целей toorun hello конкретной задачи.</span><span class="sxs-lookup"><span data-stu-id="ec240-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="ec240-186">Если требуется toobe необходимые компоненты установлены на всех узлах, независимо от hello задач, которые выполняются на нем можно использовать hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) свойства во время добавления в пул.</span><span class="sxs-lookup"><span data-stu-id="ec240-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="ec240-187">Можно использовать hello после определения задачи подготовки для ссылки.</span><span class="sxs-lookup"><span data-stu-id="ec240-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="ec240-188">Задача «Подготовка» задается во время передачи hello Azure пакетного задания.</span><span class="sxs-lookup"><span data-stu-id="ec240-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="ec240-189">Параметры конфигурации задачи подготовки Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="ec240-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="ec240-190">**Идентификатор**: Уникальный идентификатор для задачи подготовки hello</span><span class="sxs-lookup"><span data-stu-id="ec240-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="ec240-191">**Командная строка**: исполняемый файл задачи hello tooexecute командной строки</span><span class="sxs-lookup"><span data-stu-id="ec240-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="ec240-192">**resourceFiles**: массив объектов, предоставляющих подробные сведения о файлах требуется загрузить для этой задачи toorun toobe.</span><span class="sxs-lookup"><span data-stu-id="ec240-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="ec240-193">Ниже приведены его параметры.</span><span class="sxs-lookup"><span data-stu-id="ec240-193">Following are its options</span></span>
    - <span data-ttu-id="ec240-194">blobSource: hello SAS URI файла hello</span><span class="sxs-lookup"><span data-stu-id="ec240-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="ec240-195">filePath: toodownload локальный путь и сохраните файл hello</span><span class="sxs-lookup"><span data-stu-id="ec240-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="ec240-196">fileMode: применим только для узлов Linux. fileMode имеет восьмеричный формат и значение по умолчанию 0770.</span><span class="sxs-lookup"><span data-stu-id="ec240-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="ec240-197">**waitForSuccess**: Если set tootrue, задачу hello не выполняется при сбое задачи подготовки</span><span class="sxs-lookup"><span data-stu-id="ec240-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="ec240-198">**runElevated**: задать для него tootrue повышенные привилегии в случае необходимости toorun задачу hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="ec240-199">Следующий фрагмент кода показывает образец hello подготовки задачи скрипта конфигурации:</span><span class="sxs-lookup"><span data-stu-id="ec240-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="ec240-200">Если не toobe необходимые компоненты установлены для вашей toorun задачи, можно пропустить задачи подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="ec240-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="ec240-201">Следующий код создает задание с отображаемым именем process csv files.</span><span class="sxs-lookup"><span data-stu-id="ec240-201">Following code creates a job with display name "process csv files."</span></span>

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="ec240-202">Шаг 5. Отправка задач пакетной службы Azure для задания</span><span class="sxs-lookup"><span data-stu-id="ec240-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="ec240-203">Теперь, когда задание преобразования CSV-файлов создано, можно создать задачи для него.</span><span class="sxs-lookup"><span data-stu-id="ec240-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="ec240-204">Предположим, что у нас есть четыре контейнеров, у нас есть четыре задачи toocreate, один для каждого контейнера.</span><span class="sxs-lookup"><span data-stu-id="ec240-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="ec240-205">Если взглянуть на hello [сценарий Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), он принимает два параметра:</span><span class="sxs-lookup"><span data-stu-id="ec240-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="ec240-206">Имя контейнера: hello файлы toodownload контейнера хранилища из</span><span class="sxs-lookup"><span data-stu-id="ec240-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="ec240-207">pattern: необязательный параметр шаблона имени файла.</span><span class="sxs-lookup"><span data-stu-id="ec240-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="ec240-208">Предположим, что у нас есть четыре контейнеры «con1», «con2», «con3», «con4» ниже показан отправкой на задачи toohello Azure пакетного задания «процесса csv» созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="ec240-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="ec240-209">Hello код добавляет пул toohello несколько задач.</span><span class="sxs-lookup"><span data-stu-id="ec240-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="ec240-210">И каждая из задач hello выполняется на узле в пуле hello создания виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ec240-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="ec240-211">Если hello число задач превышает hello число виртуальных машин в свойстве maxTasksPerNode пула или hello, задачи hello Подождите, пока узел станет доступным.</span><span class="sxs-lookup"><span data-stu-id="ec240-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="ec240-212">Это задание оркестрации пакетная служба Azure обрабатывает автоматически.</span><span class="sxs-lookup"><span data-stu-id="ec240-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="ec240-213">портал Hello содержатся подробные представления для задач hello и состояний задания.</span><span class="sxs-lookup"><span data-stu-id="ec240-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="ec240-214">Можно также использовать список hello и функции получения в hello узла Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="ec240-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="ec240-215">Подробные сведения приведены в документации hello [ссылку](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="ec240-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec240-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec240-216">Next steps</span></span>

- <span data-ttu-id="ec240-217">Просмотрите hello [возможности пакетной обработки Обзор Azure](batch-api-basics.md) статьи, которая рекомендуется, если вы новую службу toohello.</span><span class="sxs-lookup"><span data-stu-id="ec240-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="ec240-218">. В разделе hello [ссылку пакета Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API пакета.</span><span class="sxs-lookup"><span data-stu-id="ec240-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

