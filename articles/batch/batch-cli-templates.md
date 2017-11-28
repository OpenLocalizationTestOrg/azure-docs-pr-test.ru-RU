---
title: "Комплексное выполнение пакетных заданий Azure без написания кода (предварительная версия) | Документация Майкрософт"
description: "Узнайте, как создать файлы шаблонов для Azure CLI для создания пулов, заданий и задач пакетной службы."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: 6b91466da46d1f4ca9f25bf1718be783603efc58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="3c864-103">Использование шаблонов интерфейса командной строки для пакетной службы Azure и передачи файлов (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="3c864-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="3c864-104">Интерфейс командной строки Azure позволяет выполнять пакетные задания Azure без написания кода.</span><span class="sxs-lookup"><span data-stu-id="3c864-104">Using the Azure CLI it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="3c864-105">Файлы шаблонов можно создавать и использовать с Azure CLI, что позволяет создавать пулы, задания и задачи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="3c864-105">Template files can be created and used with the Azure CLI that allow Batch pools, jobs, and tasks to be created.</span></span> <span data-ttu-id="3c864-106">Входные файлы задания можно с легкостью передать в учетную запись хранения, связанную с учетной записью пакетной службы, и выходные файлы задания — скачать.</span><span class="sxs-lookup"><span data-stu-id="3c864-106">Job input files can be easily uploaded to the storage account associated with the Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="3c864-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="3c864-107">Overview</span></span>

<span data-ttu-id="3c864-108">Это расширение Azure CLI дает возможность пользователям, которые не являются разработчиками, комплексно использовать пакетную службу.</span><span class="sxs-lookup"><span data-stu-id="3c864-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="3c864-109">Можно создавать пулы, задания и связанные с ними задачи, передавать входные данные и скачивать получаемые выходные данные — и все это без написания кода. При этом интерфейс командной строки используются напрямую или интегрируется в сценарии.</span><span class="sxs-lookup"><span data-stu-id="3c864-109">A pool can be created, input data uploaded, jobs and associated tasks created, and the resulting output data downloaded – no code required, the CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="3c864-110">Шаблоны пакетной службы работают благодаря [поддержке пакетной службы в Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation), которая позволяет указывать в JSON-файлах значения свойств для создания пулов, заданий, задач и других элементов.</span><span class="sxs-lookup"><span data-stu-id="3c864-110">Batch templates build on the [existing Batch support in the Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files to specify property values for the creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="3c864-111">Благодаря шаблонам пакетной службы к имеющимся функциям JSON-файлов добавляются следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="3c864-111">With Batch templates, the following capabilities are added over what is possible with the JSON files:</span></span>

-   <span data-ttu-id="3c864-112">Возможность определять параметры.</span><span class="sxs-lookup"><span data-stu-id="3c864-112">Parameters can be defined.</span></span> <span data-ttu-id="3c864-113">При использовании шаблона указываются только значения параметров для создания элемента, а остальные значения свойств элемента содержатся в теле шаблона.</span><span class="sxs-lookup"><span data-stu-id="3c864-113">When the template is used, only the parameter values are specified to create the item, with other item property values being specified in the template body.</span></span> <span data-ttu-id="3c864-114">Пользователь, понимающий принцип работы пакетной службы и приложений, запускаемых пакетной службой, может создавать шаблоны, указывая значения свойств пулов, заданий и задач.</span><span class="sxs-lookup"><span data-stu-id="3c864-114">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="3c864-115">Если пользователь мало знаком с пакетной службой и (или) приложениями, то ему необходимо указать только значения определенных параметров.</span><span class="sxs-lookup"><span data-stu-id="3c864-115">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="3c864-116">Фабрики задач создают одну или несколько задач, связанных с заданием, избавляя вас от необходимости создавать для них множество определений. Это значительно упрощает отправку заданий.</span><span class="sxs-lookup"><span data-stu-id="3c864-116">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="3c864-117">Для заданий необходимо предоставить файлы входных данных, а также часто создаются файлы выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3c864-117">Input data files need to be supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="3c864-118">По умолчанию с каждой учетной записью пакетной службы связывается учетная запись хранения, и вы можете легко передавать файлы в эту учетную запись хранения и обратно, используя интерфейс командной строки. Вам не нужно при этом писать код или использовать учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="3c864-118">A storage account is associated, by default, with each Batch account and files can be easily transferred to and from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="3c864-119">Например, [ffmpeg](http://ffmpeg.org/) — это популярное приложение, которое обрабатывает аудио- и видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="3c864-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="3c864-120">Можно использовать интерфейс командной строки для пакетной службы Azure, чтобы вызвать приложение ffmpeg, которое перекодирует исходные видеофайлы в файлы с другим разрешением.</span><span class="sxs-lookup"><span data-stu-id="3c864-120">The Azure Batch CLI can be used to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="3c864-121">Создается шаблон пула.</span><span class="sxs-lookup"><span data-stu-id="3c864-121">A pool template is created.</span></span> <span data-ttu-id="3c864-122">Пользователь, создающий шаблон, должен знать, как вызвать приложение ffmpeg и какие его требования. Необходимо указать соответствующую операционную систему, размер виртуальной машины, как было установлено приложение (например, из пакета приложения или с помощью диспетчера пакетов) и другие значения свойств пула.</span><span class="sxs-lookup"><span data-stu-id="3c864-122">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="3c864-123">Создаются параметры, таким образом при использовании шаблона необходимо указать только идентификатор пула и число виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="3c864-123">Parameters are created so when the template is used, only the pool id and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="3c864-124">Создается шаблон задания.</span><span class="sxs-lookup"><span data-stu-id="3c864-124">A job template is created.</span></span> <span data-ttu-id="3c864-125">Пользователь, создающий шаблон, должен знать, как вызвать приложение ffmpeg для перекодирования исходного видео в файл с другим разрешением и указать командную строку задачи. Он также должен знать, что существует папка, в которой содержатся исходные видеофайлы, и что для каждого входного файла требуется одна задача.</span><span class="sxs-lookup"><span data-stu-id="3c864-125">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="3c864-126">Сначала пользователь создает пул для набора видеофайлов, которые необходимо перекодировать. Он использует шаблон пула, указывая только идентификатор пула и требуемое число виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="3c864-126">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool id and number of VMs required.</span></span> <span data-ttu-id="3c864-127">После этого можно передать исходные файлы для перекодирования.</span><span class="sxs-lookup"><span data-stu-id="3c864-127">They can then upload the source files to transcode.</span></span> <span data-ttu-id="3c864-128">Затем с помощью шаблона задания можно отправить задание, указав только идентификатор пула и расположение переданных исходных файлов.</span><span class="sxs-lookup"><span data-stu-id="3c864-128">A job can then be submitted using the job template, specifying only the pool id and location of the source files uploaded.</span></span> <span data-ttu-id="3c864-129">Создается пакетное задание. Для каждого входного файла создается одна задача.</span><span class="sxs-lookup"><span data-stu-id="3c864-129">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="3c864-130">Наконец, можно скачать перекодированные выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="3c864-130">Finally, the transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="3c864-131">Установка</span><span class="sxs-lookup"><span data-stu-id="3c864-131">Installation</span></span>

<span data-ttu-id="3c864-132">Для использования функций шаблонов и передачи файлов требуется установить расширение.</span><span class="sxs-lookup"><span data-stu-id="3c864-132">The template and file transfer capabilities require an extension to be installed.</span></span>

<span data-ttu-id="3c864-133">Инструкции по установке Azure CLI см. на [этой странице](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3c864-133">For instructions on how to install the Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="3c864-134">После установки Azure CLI вы можете установить расширение пакетной службы с помощью следующей команды CLI:</span><span class="sxs-lookup"><span data-stu-id="3c864-134">Once the Azure CLI has been installed, the Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="3c864-135">Дополнительные сведения о расширении пакетной службы см. в статье [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux) (Расширения командной строки для пакетной службы Microsoft Azure для Windows, Mac и Linux).</span><span class="sxs-lookup"><span data-stu-id="3c864-135">For more information about the Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="3c864-136">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="3c864-136">Templates</span></span>

<span data-ttu-id="3c864-137">Интерфейс командной строки для пакетной службы Azure позволяет создавать элементы, такие как пулы, задания и задачи, указав JSON-файл, в котором содержатся имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="3c864-137">The Azure Batch CLI allows items such as pools, jobs, and tasks to be created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="3c864-138">Например:</span><span class="sxs-lookup"><span data-stu-id="3c864-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="3c864-139">Шаблоны пакетной службы Azure по функциональности и синтаксису похожи на шаблоны Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3c864-139">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="3c864-140">Они являются JSON-файлами, содержащими имена и значения свойств элементов, но в них добавлены следующие основные понятия:</span><span class="sxs-lookup"><span data-stu-id="3c864-140">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="3c864-141">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="3c864-141">**Parameters**</span></span>

    -   <span data-ttu-id="3c864-142">Позволяют указывать значения свойств в теле шаблона. При использовании шаблона необходимо предоставить только значения параметров.</span><span class="sxs-lookup"><span data-stu-id="3c864-142">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="3c864-143">Например, полное определение пула можно поместить в тело и определить только один параметр для идентификатора пула. Таким образом, для создания пула необходимо указать только строку идентификатора пула.</span><span class="sxs-lookup"><span data-stu-id="3c864-143">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool id string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="3c864-144">Тело шаблона может создать пользователь, который знаком с пакетной службой и приложениями, запускаемыми пакетной службой. При использовании шаблона необходимо указать только значения параметров, определенных создателем шаблона.</span><span class="sxs-lookup"><span data-stu-id="3c864-144">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="3c864-145">Поэтому пользователь, мало знакомый с пакетной службой и (или) приложениями, также может использовать шаблоны.</span><span class="sxs-lookup"><span data-stu-id="3c864-145">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="3c864-146">**Переменные**</span><span class="sxs-lookup"><span data-stu-id="3c864-146">**Variables**</span></span>

    -   <span data-ttu-id="3c864-147">Позволяют указывать значения простых или сложных параметров в одном месте, а затем использовать их в одном или нескольких местах в теле шаблона.</span><span class="sxs-lookup"><span data-stu-id="3c864-147">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="3c864-148">С помощью переменных можно упростить шаблон и уменьшить его размер, а также сделать его более удобным в использовании благодаря возможности в одном месте изменять свойства, значения которых могут меняться.</span><span class="sxs-lookup"><span data-stu-id="3c864-148">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties whose value may change.</span></span>

-   <span data-ttu-id="3c864-149">**Конструкции более высокого уровня**</span><span class="sxs-lookup"><span data-stu-id="3c864-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="3c864-150">В шаблоне доступны некоторые конструкции более высокого уровня, которые еще не доступны в интерфейсах API пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="3c864-150">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="3c864-151">Например, в шаблоне задания на основе стандартного определения задач можно определить фабрику задач, которая создаст несколько задач для одного задания.</span><span class="sxs-lookup"><span data-stu-id="3c864-151">For example, a task factory can be defined in a job template that creates multiple tasks for the job using a common task definition.</span></span> <span data-ttu-id="3c864-152">Благодаря этим конструкциям не требуется писать код, чтобы динамически создать несколько JSON-файлов, например по одному файлу для каждой задачи, или создавать файлы сценариев для установки приложений через диспетчер пакетов.</span><span class="sxs-lookup"><span data-stu-id="3c864-152">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="3c864-153">На определенном этапе (где это применимо) данные конструкции можно добавить в пакетную службу, сделав их доступными через интерфейсы API пакетной службы, пользовательские интерфейсы и т. д.</span><span class="sxs-lookup"><span data-stu-id="3c864-153">At some point, where applicable, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="3c864-154">Шаблоны пула</span><span class="sxs-lookup"><span data-stu-id="3c864-154">Pool templates</span></span>

<span data-ttu-id="3c864-155">Помимо стандартных возможностей шаблонов (параметры и переменные) шаблон пула поддерживает следующие конструкции более высокого уровня:</span><span class="sxs-lookup"><span data-stu-id="3c864-155">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the pool template:</span></span>

-   <span data-ttu-id="3c864-156">**Ссылки на пакет**</span><span class="sxs-lookup"><span data-stu-id="3c864-156">**Package references**</span></span>

    -   <span data-ttu-id="3c864-157">Позволяют при необходимости копировать программное обеспечение в узлы пула с помощью диспетчеров пакетов.</span><span class="sxs-lookup"><span data-stu-id="3c864-157">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="3c864-158">Указываются диспетчер пакетов и идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="3c864-158">The package manager and package id are specified.</span></span> <span data-ttu-id="3c864-159">Возможность объявить про один или несколько пакетов избавляет от необходимости создавать сценарий, который получает пакеты, устанавливать этот сценарий и запускать его на каждом узле пула.</span><span class="sxs-lookup"><span data-stu-id="3c864-159">Being able to declare one or more packages avoids the need to create a script that gets the required packages, install the script, and run the script on each pool node.</span></span>

<span data-ttu-id="3c864-160">Ниже приведен пример шаблона, который создает пул виртуальных машин Linux с установленным приложением ffmpeg. Ему требуется только строка идентификатора пула и число виртуальных машин, которое необходимо предоставить для использования.</span><span class="sxs-lookup"><span data-stu-id="3c864-160">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and the number of VMs to be supplied to use:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="3c864-161">Если имя файла шаблона — _pool-ffmpeg.json_, то шаблон будет вызываться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3c864-161">If the template file was named _pool-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="3c864-162">Шаблоны задания</span><span class="sxs-lookup"><span data-stu-id="3c864-162">Job templates</span></span>

<span data-ttu-id="3c864-163">Помимо стандартных возможностей шаблонов (параметры и переменные) шаблон задания поддерживает следующие конструкции более высокого уровня:</span><span class="sxs-lookup"><span data-stu-id="3c864-163">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the job template:</span></span>

-   <span data-ttu-id="3c864-164">**Фабрика задач**</span><span class="sxs-lookup"><span data-stu-id="3c864-164">**Task factory**</span></span>

    -   <span data-ttu-id="3c864-165">Создает несколько задач для одного задания, используя одно определение задачи.</span><span class="sxs-lookup"><span data-stu-id="3c864-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="3c864-166">Поддерживается три типа фабрики задач: параметрический анализ, "по одной задаче на файл" и коллекция задач.</span><span class="sxs-lookup"><span data-stu-id="3c864-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="3c864-167">Ниже приведен пример шаблона, который создает задание, использующее приложение ffmpeg для перекодирования видеофайлов MP4 в один из двух форматов с более низким разрешением. На каждый исходный видеофайл создается по одной задаче.</span><span class="sxs-lookup"><span data-stu-id="3c864-167">The following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files to one of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="3c864-168">Если имя файла шаблона — _job-ffmpeg.json_, то шаблон будет вызываться следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3c864-168">If the template file was named _job-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="3c864-169">Группы файлов и передача файлов</span><span class="sxs-lookup"><span data-stu-id="3c864-169">File groups and file transfer</span></span>

<span data-ttu-id="3c864-170">Большинство заданий и задач принимают входные файлы и создают выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="3c864-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="3c864-171">Обычно входные и выходные файлы должны быть переданы от клиента на узел или с узла клиенту.</span><span class="sxs-lookup"><span data-stu-id="3c864-171">Both input files and output files typically need to be transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="3c864-172">Расширение интерфейса командной строки для пакетной службы Azure значительно упрощает передачу файлов и использует учетную запись хранения, которая по умолчанию создается для каждой учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="3c864-172">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="3c864-173">Группа файлов соответствует контейнеру, создаваемому в учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="3c864-173">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="3c864-174">Группа файлов может иметь вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="3c864-174">The file group may have subfolders.</span></span>

<span data-ttu-id="3c864-175">Расширение CLI для пакетной службы предоставляет команды, которые позволяют передать файлы от клиента в указанную группу файлов или скачать в клиент файлы из указанной группы файлов.</span><span class="sxs-lookup"><span data-stu-id="3c864-175">The Batch CLI extension provides commands for uploading files from client to a specified file group and downloading files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="3c864-176">Шаблоны пула и задания позволяют указать файлы, хранящиеся в группах файлов, для копирования на узлы пула или с узлов пула обратно в группу файлов.</span><span class="sxs-lookup"><span data-stu-id="3c864-176">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="3c864-177">Например, в приведенном выше шаблоне задания группа файлов ffmpeg-input указывается для фабрики задач как расположение исходных видеофайлов, которые копируются на узел для перекодирования. Группа файлов ffmpeg-output используется в качестве расположения, в которое копируются перекодированные выходные файлы из узла при выполнении каждой задачи.</span><span class="sxs-lookup"><span data-stu-id="3c864-177">For example, in the job template specified previously, the file group “ffmpeg-input” is specified for the task factory as the location of the source video files copied down onto the node for transcoding; the file group “ffmpeg-output” is used as the location where the transcoded output files are copied to from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="3c864-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="3c864-178">Summary</span></span>

<span data-ttu-id="3c864-179">Сейчас поддержка шаблонов и передачи файлов реализована только в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3c864-179">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="3c864-180">В будущем планируется расширить аудиторию пакетной службы до пользователей, которым не нужно разрабатывать код, используя интерфейсы API пакетной службы, например исследователей, ИТ-пользователи и т. д.</span><span class="sxs-lookup"><span data-stu-id="3c864-180">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="3c864-181">Пользователи, знакомые с Azure, пакетной службой и приложениями, которые запускает пакетная служба, могут создавать шаблоны для создания пулов и заданий, не прибегая к написанию кода.</span><span class="sxs-lookup"><span data-stu-id="3c864-181">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="3c864-182">Параметры шаблона позволяют использовать шаблоны даже пользователям с небольшим опытом работы с пакетной службой и приложениями.</span><span class="sxs-lookup"><span data-stu-id="3c864-182">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="3c864-183">Попробуйте использовать расширение пакетной службы для Azure CLI и оставьте отзыв или предложения в комментариях к этой статье или на [форуме по пакетной службе Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="3c864-183">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c864-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c864-184">Next steps</span></span>

- <span data-ttu-id="3c864-185">Прочитайте запись блога о пакетной службе: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/) (Выполнение пакетных заданий Azure с помощью Azure CLI без написания кода).</span><span class="sxs-lookup"><span data-stu-id="3c864-185">See the Batch templates blog post: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="3c864-186">Подробная документация по установке и использованию, примеры и исходный код доступны в [репозитории Azure GitHub](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="3c864-186">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
