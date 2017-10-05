---
title: "Руководство. Использование клиентской библиотеки пакетной службы Azure для Node.js | Документация Майкрософт"
description: "Изучите основные принципы работы пакетной службы Azure и создайте простое решение с использованием Node.js."
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
ms.openlocfilehash: c48171d8634a651718a0775183414f463c6a468c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="ffc2f-103">Приступая к работе с пакетом SDK для пакетной службы для Node.js</span><span class="sxs-lookup"><span data-stu-id="ffc2f-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ffc2f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ffc2f-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="ffc2f-105">Python</span><span class="sxs-lookup"><span data-stu-id="ffc2f-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="ffc2f-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="ffc2f-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="ffc2f-107">Изучите основы создания клиента пакетной службы в Node.js с помощью [пакета SDK для пакетной службы Azure для Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-107">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="ffc2f-108">Мы определим ключевые аспекты приложения пакетной службы, а затем настроим его с помощью клиента Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ffc2f-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ffc2f-109">Prerequisites</span></span>
<span data-ttu-id="ffc2f-110">В этой статье предполагается, что вы уже работали с Node.js и знаете, как работать в Linux.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="ffc2f-111">Также предполагается, что у вас есть настроенная учетная запись Azure с правами доступа для создания пакетной службы и службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-111">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="ffc2f-112">Перед изучением шагов, описанных в этой статье, советуем ознакомиться со статьей [Выполнение реальных параллельных рабочих нагрузок с использованием пакетной службы](batch-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="ffc2f-113">Рассматриваемый сценарий</span><span class="sxs-lookup"><span data-stu-id="ffc2f-113">The tutorial scenario</span></span>
<span data-ttu-id="ffc2f-114">Рассмотрим сценарий рабочего процесса пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-114">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="ffc2f-115">У нас есть простой скрипт, написанный на языке Python, который загружает все CSV-файлы из контейнера хранилища BLOB-объектов Azure и преобразует их в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="ffc2f-116">Для параллельной обработки нескольких контейнеров учетных записей хранения можно развернуть скрипт как задание пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-116">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="ffc2f-117">Архитектура пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ffc2f-117">Azure Batch Architecture</span></span>
<span data-ttu-id="ffc2f-118">На следующей схеме показано, как можно масштабировать скрипт Python с помощью пакетной службы Azure и клиента Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-118">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Сценарий пакетной службы Azure](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="ffc2f-120">Клиент Node.js развертывает задание пакетной службы с задачей подготовки (описанной далее) и набор задач в зависимости от числа контейнеров в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-120">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="ffc2f-121">Скрипты можно скачать из репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-121">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="ffc2f-122">Клиент Node.js</span><span class="sxs-lookup"><span data-stu-id="ffc2f-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="ffc2f-123">Скрипты оболочки для задач подготовки</span><span class="sxs-lookup"><span data-stu-id="ffc2f-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="ffc2f-124">Преобразователь Python CSV в JSON</span><span class="sxs-lookup"><span data-stu-id="ffc2f-124">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="ffc2f-125">Клиент Node.js по указанной ссылке не содержит код, который необходимо развертывать в качестве приложения-функции Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-125">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="ffc2f-126">Перейдите по следующим ссылкам, чтобы ознакомиться с инструкциями по его созданию.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-126">You can refer to the following links for instructions to create one.</span></span>
> - [<span data-ttu-id="ffc2f-127">Создание приложения-функции</span><span class="sxs-lookup"><span data-stu-id="ffc2f-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="ffc2f-128">Триггер таймера</span><span class="sxs-lookup"><span data-stu-id="ffc2f-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a><span data-ttu-id="ffc2f-129">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="ffc2f-129">Build the application</span></span>

<span data-ttu-id="ffc2f-130">Рассмотрим пошаговый процесс создания клиента Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-130">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="ffc2f-131">Шаг 1. Установка пакета SDK для пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ffc2f-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="ffc2f-132">Пакет SDK для пакетной службы Azure для Node.js можно установить с помощью команды npm install.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-132">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="ffc2f-133">Эта команда устанавливает последнюю версию пакета SDK узла azure-batch.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-133">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="ffc2f-134">Для запуска команд npm install в приложении-функции Azure перейдите к консоли Kudu на вкладке параметров функций Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-134">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="ffc2f-135">В этом случае для установки пакета SDK для пакетной службы Azure для Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-135">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="ffc2f-136">Шаг 2. Создание учетной записи пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ffc2f-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="ffc2f-137">Ее можно создать на портале [Azure](batch-account-create-portal.md) или с помощью командной строки ([PowerShell](batch-powershell-cmdlets-get-started.md)  / [Azure CLI](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-137">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="ffc2f-138">Ниже перечислены команды для создания учетной записи пакетной службы Azure с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-138">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="ffc2f-139">Создайте группу ресурсов. (Пропустите этот шаг, если у вас уже есть группа, в которой вы хотите создать учетную запись пакетной службы.)</span><span class="sxs-lookup"><span data-stu-id="ffc2f-139">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="ffc2f-140">Создайте учетную запись пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="ffc2f-141">Каждая учетная запись пакетной службы имеет соответствующие ключи доступа.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="ffc2f-142">Эти ключи необходимы для создания дополнительных ресурсов в учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-142">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="ffc2f-143">В рабочей среде рекомендуется использовать Azure Key Vault для хранения этих ключей.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-143">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="ffc2f-144">Теперь необходимо создать субъект-службу для приложения.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-144">You can then create a Service principal for the application.</span></span> <span data-ttu-id="ffc2f-145">С помощью этого субъекта-службы приложение может создать токен OAuth для доступа к ключам из хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-145">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="ffc2f-146">Скопируйте и сохраните ключ, который будет использоваться на последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-146">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="ffc2f-147">Шаг 3. Создание клиента пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ffc2f-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="ffc2f-148">Следующий фрагмент кода сначала импортирует модуль Node.js azure-batch, а затем создает клиент пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-148">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="ffc2f-149">Сначала необходимо создать объект SharedKeyCredentials, используя ключ учетной записи пакетной службы, скопированный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-149">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

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

<span data-ttu-id="ffc2f-150">URI пакетной службы Azure можно найти на вкладке "Обзор" на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-150">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="ffc2f-151">Он имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="ffc2f-151">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="ffc2f-152">См. снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="ffc2f-152">Refer to the screenshot:</span></span>

![URI пакетной службы Azure](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="ffc2f-154">Шаг 4. Создание пула пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ffc2f-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="ffc2f-155">Пул пакетной службы Azure состоит из нескольких виртуальных машин (также известных как узлы пакетной службы).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="ffc2f-156">На этих узлах пакетная служба Azure развертывает задачи и управляет ими.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-156">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="ffc2f-157">Задайте следующие параметры конфигурации для пула:</span><span class="sxs-lookup"><span data-stu-id="ffc2f-157">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="ffc2f-158">тип образа виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="ffc2f-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="ffc2f-159">размер узлов виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="ffc2f-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="ffc2f-160">число узлов виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="ffc2f-161">Размер и количество узлов виртуальной машины во многом зависит от числа задач, которые требуется выполнить параллельно, а также от самой задачи.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-161">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="ffc2f-162">Мы советуем провести тестирование для определения идеального количества и размера.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-162">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="ffc2f-163">Следующий фрагмент кода создает объекты параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-163">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="ffc2f-164">Список образов виртуальных машин Linux для пакетной службы Azure и соответствующие номера SKU см. в разделе [Список образов виртуальных машин](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-164">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="ffc2f-165">После определения конфигурации можно создать пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-165">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="ffc2f-166">Команда пула пакетной службы создает узлы виртуальных машин Azure и подготавливает их к получению задач для выполнения.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-166">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="ffc2f-167">Каждый пул должен иметь уникальный идентификатор, чтобы на него можно было ссылаться на последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="ffc2f-168">Следующий фрагмент кода создает пул пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-168">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="ffc2f-169">Убедитесь, что пул находится в активном состоянии, прежде чем отправить в него задание.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-169">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

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

<span data-ttu-id="ffc2f-170">Ниже приведен пример результирующего объекта, возвращаемого функцией pool.get.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-170">Following is a sample result object returned by the pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="ffc2f-171">Шаг 4. Отправка задания пакетной службы Azure</span><span class="sxs-lookup"><span data-stu-id="ffc2f-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="ffc2f-172">Задание пакетной службы Azure представляет собой логическую группу схожих задач.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="ffc2f-173">В нашем случае это преобразование CSV в JSON.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-173">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="ffc2f-174">В нем каждая задача может обрабатывать CSV-файлы, которые присутствуют в каждом контейнере службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="ffc2f-175">Эти задачи могут выполняться параллельно и развертываться на нескольких узлах, управляемых пакетной службой Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="ffc2f-176">Чтобы указать максимальное число задач, которые могут выполняться параллельно на одном узле, используйте свойство [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-176">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="ffc2f-177">Задача подготовки</span><span class="sxs-lookup"><span data-stu-id="ffc2f-177">Preparation task</span></span>

<span data-ttu-id="ffc2f-178">Созданные узлы виртуальных машин являются пустыми узлами Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-178">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="ffc2f-179">Часто необходимо установить набор программ в качестве необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-179">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="ffc2f-180">Обычно для узлов Linux можно использовать скрипт оболочки, который устанавливает необходимые компоненты перед запуском фактических задач.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-180">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="ffc2f-181">Однако это может быть любой программируемый исполняемый файл.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="ffc2f-182">[Скрипт оболочки](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) в этом примере устанавливает Python-pip и пакет SDK для службы хранилища Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-182">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="ffc2f-183">Можно отправить скрипт в учетную запись хранения Azure и создать URI SAS для доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-183">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="ffc2f-184">Этот процесс можно автоматизировать с помощью пакета SDK для службы хранилища Azure для Node.js.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-184">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="ffc2f-185">Задача подготовки задания выполняется только на узлах виртуальных машин, где необходимо выполнить определенную задачу.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-185">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="ffc2f-186">Если требуемые компоненты нужно установить на всех узлах независимо от выполняемых задач, при добавлении пула можно использовать свойство [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-186">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="ffc2f-187">Для справки можно использовать следующее определение задачи подготовки.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-187">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="ffc2f-188">Задача подготовки указывается во время отправки задания пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-188">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="ffc2f-189">Ниже перечислены параметры конфигурации задачи подготовки.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-189">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="ffc2f-190">**ID:** уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-190">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="ffc2f-191">**commandLine:** командная строка для выполнения исполняемого файла задачи.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-191">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="ffc2f-192">**resourceFiles:** массив объектов, предоставляющих сведения о файлах, которые нужно скачать для выполнения этой задачи.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-192">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="ffc2f-193">Ниже приведены его параметры.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-193">Following are its options</span></span>
    - <span data-ttu-id="ffc2f-194">blobSource: URI SAS файла.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-194">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="ffc2f-195">filePath: локальный путь для скачивания и сохранения файла.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-195">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="ffc2f-196">fileMode: применим только для узлов Linux. fileMode имеет восьмеричный формат и значение по умолчанию 0770.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="ffc2f-197">**waitForSuccess:** если задано значение true, задача не выполняется при сбое задачи подготовки.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-197">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="ffc2f-198">**runElevated:** задайте значение true, если для выполнения задачи требуются повышенные привилегии.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-198">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="ffc2f-199">В следующем фрагменте кода показан пример конфигурации скрипта задачи подготовки:</span><span class="sxs-lookup"><span data-stu-id="ffc2f-199">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="ffc2f-200">Если обязательных компонентов, которые необходимо установить для выполнения задач, нет, задачи подготовки можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-200">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="ffc2f-201">Следующий код создает задание с отображаемым именем process csv files.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="ffc2f-202">Шаг 5. Отправка задач пакетной службы Azure для задания</span><span class="sxs-lookup"><span data-stu-id="ffc2f-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="ffc2f-203">Теперь, когда задание преобразования CSV-файлов создано, можно создать задачи для него.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="ffc2f-204">Предположим, у нас есть четыре контейнера, для каждого из которых необходимо создать задачу.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-204">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="ffc2f-205">[Скрипт Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py) принимает два параметра:</span><span class="sxs-lookup"><span data-stu-id="ffc2f-205">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="ffc2f-206">container_name: контейнер хранилища, откуда будут скачиваться файлы.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-206">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="ffc2f-207">pattern: необязательный параметр шаблона имени файла.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="ffc2f-208">Предположим, у нас есть четыре контейнера con1, con2, con3, con4. Следующий код отправляет задачи в задание пакетной службы Azure process csv, созданное ранее.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="ffc2f-209">Код добавляет несколько задач в пул.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-209">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="ffc2f-210">Все задачи выполняются на узле созданного пула виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-210">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="ffc2f-211">Если количество задач превышает число виртуальных машин в пуле или значение свойства maxTasksPerNode, задачи ожидают, пока узел станет доступным.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-211">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="ffc2f-212">Это задание оркестрации пакетная служба Azure обрабатывает автоматически.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="ffc2f-213">Портал содержит подробные представления задач и состояния заданий.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-213">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="ffc2f-214">Можно также использовать список, чтобы получить функции в пакете SDK узла Azure.</span><span class="sxs-lookup"><span data-stu-id="ffc2f-214">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="ffc2f-215">Подробные сведения приведены в документации по [ссылке](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-215">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffc2f-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffc2f-216">Next steps</span></span>

- <span data-ttu-id="ffc2f-217">Если вы недавно используете пакетную службу, рекомендуем прочитать статью [с обзором функций пакетной службы Azure](batch-api-basics.md) .</span><span class="sxs-lookup"><span data-stu-id="ffc2f-217">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="ffc2f-218">Сведения об API пакетной службы см. в статье [Microsoft Azure SDK for Node.js - Batch Service](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) (Пакет Microsoft Azure SDK для Node.js. Пакетная служба).</span><span class="sxs-lookup"><span data-stu-id="ffc2f-218">See the [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) to explore the Batch API.</span></span>

