---
title: "aaaRun Azure пакетных заданий конца в конец без написания кода (Предварительная версия) | Документы Microsoft"
description: "Создайте файлы шаблонов для hello Azure CLI toocreate пакета пулы, заданий и задач."
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
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="21f83-103">Использование шаблонов интерфейса командной строки для пакетной службы Azure и передачи файлов (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="21f83-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="21f83-104">При помощи hello Azure CLI можно возможных toorun пакетных заданий без написания кода.</span><span class="sxs-lookup"><span data-stu-id="21f83-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="21f83-105">Файлы шаблонов можно создать и использовать с hello Azure CLI, разрешить пулы, задания и toobe задачи создания пакета.</span><span class="sxs-lookup"><span data-stu-id="21f83-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="21f83-106">Задание входных файлов можно легко загрузить учетную запись хранилища hello, связанную с hello пакетной учетной записи и задание выходные файлы загружаются.</span><span class="sxs-lookup"><span data-stu-id="21f83-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="21f83-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="21f83-107">Overview</span></span>

<span data-ttu-id="21f83-108">Расширение toohello Azure CLI позволяет пакета используется toobe-законченный пользователями, которые не являются разработчиками.</span><span class="sxs-lookup"><span data-stu-id="21f83-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="21f83-109">Можно создать пул, передачи входных данных задания и связанные с ними задачи создания и CLI hello hello результирующие выходные данные загружаются — код не требуется, используются непосредственно, или нужно интегрировать в сценарии.</span><span class="sxs-lookup"><span data-stu-id="21f83-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="21f83-110">Построение пакета шаблоны на hello [существующего пакета поддержки в hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) JSON-файлов, позволяющий toospecify значения свойств для создания hello пулы, заданий, задач и других элементов.</span><span class="sxs-lookup"><span data-stu-id="21f83-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="21f83-111">С помощью шаблонов пакета hello следующие возможности добавляются по возможности файлы hello JSON:</span><span class="sxs-lookup"><span data-stu-id="21f83-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="21f83-112">Возможность определять параметры.</span><span class="sxs-lookup"><span data-stu-id="21f83-112">Parameters can be defined.</span></span> <span data-ttu-id="21f83-113">При использовании шаблона hello только значения параметра hello, элемента указанного toocreate hello и другие значения свойства элемента, указанными в тексте hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="21f83-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="21f83-114">Пользователь, который понимает, что пакет и toobe приложения выполнялись пакета можно создать шаблоны, указывая пул, задания и значения свойств задачи.</span><span class="sxs-lookup"><span data-stu-id="21f83-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="21f83-115">Пользователю меньше знакомые с приложениями и пакете достаточно toospecify hello значения для параметров определенных hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="21f83-116">Для многих toobe определения задач создания и значительно упрощения процесса отправки заданий создания фабрики задач задания или дополнительные задачи, связанные с заданием, как избежать hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="21f83-117">Файлы входные данные должны toobe, указанное для задания, и часто создаваемых выходных файлов данных.</span><span class="sxs-lookup"><span data-stu-id="21f83-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="21f83-118">Связанные учетной записи хранения по умолчанию, при этом каждый пакет учетной записи и файлы могут быть легко переносятся tooand с этой учетной записи хранилища, используя интерфейс командной строки, без написания кода и необходимые без учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="21f83-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="21f83-119">Например, [ffmpeg](http://ffmpeg.org/) — это популярное приложение, которое обрабатывает аудио- и видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="21f83-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="21f83-120">Hello Azure CLI пакета может быть используется tooinvoke ffmpeg tootranscode источника видеофайлов toodifferent способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="21f83-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="21f83-121">Создается шаблон пула.</span><span class="sxs-lookup"><span data-stu-id="21f83-121">A pool template is created.</span></span> <span data-ttu-id="21f83-122">Создание шаблона hello пользователя Hello знает, как toocall hello ffmpeg приложения и его требования; они задают hello соответствующие операционной системы, ВМ размер, как ffmpeg установлен (из пакета приложения или с помощью диспетчера пакетов, например) и другие значения свойств пула.</span><span class="sxs-lookup"><span data-stu-id="21f83-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="21f83-123">Поэтому при использовании шаблона hello только идентификатор пула hello и число виртуальных машин требуется toobe указан, создаются параметры.</span><span class="sxs-lookup"><span data-stu-id="21f83-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="21f83-124">Создается шаблон задания.</span><span class="sxs-lookup"><span data-stu-id="21f83-124">A job template is created.</span></span> <span data-ttu-id="21f83-125">Создание шаблона hello Hello пользователя знает, как вызывается tootranscode источник видео tooa другое разрешение toobe ffmpeg потребностей и указывает hello задачи командной строки; они также показывает, что папка, содержащая hello источника видеофайлов, с задачей, которая требуется для каждого входного файла.</span><span class="sxs-lookup"><span data-stu-id="21f83-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="21f83-126">Пользователь с набором tootranscode видеофайлов сначала создает пул с помощью шаблона пула hello, указав только идентификатор пула hello и число необходимых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="21f83-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="21f83-127">Их можно будет передать файлы tootranscode hello источника.</span><span class="sxs-lookup"><span data-stu-id="21f83-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="21f83-128">Затем можно отправить задание с помощью шаблона задания hello, указав только идентификатор пула hello и загруженных файлов источника hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="21f83-129">Hello пакетное задание создается с одну задачу на создаваемый входного файла.</span><span class="sxs-lookup"><span data-stu-id="21f83-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="21f83-130">Наконец Привет перекодировать выходные файлы можно загрузить.</span><span class="sxs-lookup"><span data-stu-id="21f83-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="21f83-131">Установка</span><span class="sxs-lookup"><span data-stu-id="21f83-131">Installation</span></span>

<span data-ttu-id="21f83-132">возможности передачи шаблон и файл Hello требуют toobe модуль установлен.</span><span class="sxs-lookup"><span data-stu-id="21f83-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="21f83-133">Инструкции по tooinstall hello Azure CLI. в статье [установить CLI Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="21f83-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="21f83-134">Один раз приветствия установил Azure CLI hello пакета могут быть установлены расширения с помощью следующей команды CLI:</span><span class="sxs-lookup"><span data-stu-id="21f83-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="21f83-135">Дополнительные сведения о hello пакета расширения в разделе [Microsoft Azure пакета CLI расширения для Windows, Mac и Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="21f83-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="21f83-136">Шаблоны</span><span class="sxs-lookup"><span data-stu-id="21f83-136">Templates</span></span>

<span data-ttu-id="21f83-137">Hello Azure CLI пакета позволяет пулы, заданий и toobe задачи, созданные путем указания JSON-файл, содержащий имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="21f83-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="21f83-138">Например:</span><span class="sxs-lookup"><span data-stu-id="21f83-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="21f83-139">Шаблоны пакета Azure являются похожих шаблонов диспетчера ресурсов tooAzure в функции и синтаксис.</span><span class="sxs-lookup"><span data-stu-id="21f83-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="21f83-140">Они представляют собой файлы JSON содержат элемент имена и значения свойств, но добавить hello следующих основных понятиях:</span><span class="sxs-lookup"><span data-stu-id="21f83-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="21f83-141">**Параметры**</span><span class="sxs-lookup"><span data-stu-id="21f83-141">**Parameters**</span></span>

    -   <span data-ttu-id="21f83-142">Разрешить toobe значения свойства, указанный в разделе "текст", со значениями параметров, создающие toobe, предоставленный при использовании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="21f83-143">Например полное определение hello в пуле может быть размещен в тексте hello и только один параметр, определенных для идентификатора пула; только строка идентификатора пула таким образом, необходим toocreate toobe указан пул.</span><span class="sxs-lookup"><span data-stu-id="21f83-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="21f83-144">текста Hello шаблона могут быть созданы пользователем, имеющим базы знаний пакета и toobe приложения hello выполнялись пакета; При использовании шаблона hello, необходимо указать только значения для параметров, определенных автором hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="21f83-145">Пользователь без hello подробные пакета и/или базы знаний приложения таким образом можно использовать шаблоны.</span><span class="sxs-lookup"><span data-stu-id="21f83-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="21f83-146">**Переменные**</span><span class="sxs-lookup"><span data-stu-id="21f83-146">**Variables**</span></span>

    -   <span data-ttu-id="21f83-147">Разрешить простые или сложные параметр toobe значения, указанные в одном месте и используются в одной или нескольких частях текста hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="21f83-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="21f83-148">Переменные можно упростить и сократить размер hello hello шаблона, а также сделать его более простого в сопровождении, задав одно расположение toochange свойства, значение которого может измениться.</span><span class="sxs-lookup"><span data-stu-id="21f83-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="21f83-149">**Конструкции более высокого уровня**</span><span class="sxs-lookup"><span data-stu-id="21f83-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="21f83-150">Некоторые конструкции более высокого уровня, доступные в hello шаблон, который еще не доступны в API-интерфейсы пакета hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="21f83-151">Например в шаблоне задания, который создает несколько задач для hello задания с помощью общего определения задач можно определить фабрики задач.</span><span class="sxs-lookup"><span data-stu-id="21f83-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="21f83-152">Эти конструкции избежать toocode необходимость hello динамически создать несколько файлов JSON, например, один файл для каждой задачи, а также создать скрипт, файлы приложений tooinstall через диспетчер пакетов, например.</span><span class="sxs-lookup"><span data-stu-id="21f83-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="21f83-153">Некоторые точки, где применимо, возможно, эти конструкции добавлена toothe пакета службы и доступен в hello API-интерфейсы пакета, пользовательских интерфейсов, и т. д.</span><span class="sxs-lookup"><span data-stu-id="21f83-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="21f83-154">Шаблоны пула</span><span class="sxs-lookup"><span data-stu-id="21f83-154">Pool templates</span></span>

<span data-ttu-id="21f83-155">Кроме возможности стандартных шаблонов toohello параметров и переменных, hello следующие высокоуровневые конструкции поддерживаются hello пула шаблон:</span><span class="sxs-lookup"><span data-stu-id="21f83-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="21f83-156">**Ссылки на пакет**</span><span class="sxs-lookup"><span data-stu-id="21f83-156">**Package references**</span></span>

    -   <span data-ttu-id="21f83-157">При необходимости менеджеры узлы toopool toobe копирования программного обеспечения с помощью пакета.</span><span class="sxs-lookup"><span data-stu-id="21f83-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="21f83-158">указаны диспетчера пакетов Hello и идентификатор пакета.</span><span class="sxs-lookup"><span data-stu-id="21f83-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="21f83-159">Может toodeclare, один или несколько пакетов позволяет избежать необходимости hello toocreate сценарий, который возвращает hello необходимые пакеты, hello скрипт установки и запустить скрипт hello на каждом узле пула.</span><span class="sxs-lookup"><span data-stu-id="21f83-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="21f83-160">следующие Hello состоит в том пример шаблона, который используется для создания пула виртуальных машин Linux с ffmpeg установлены и только требует пула идентификатор строки и hello ряд toouse toobe предоставленный виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="21f83-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
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

<span data-ttu-id="21f83-161">Если файл шаблона hello назывался _ffmpeg.json пула_, то шаблон hello будет вызываться, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="21f83-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="21f83-162">Шаблоны задания</span><span class="sxs-lookup"><span data-stu-id="21f83-162">Job templates</span></span>

<span data-ttu-id="21f83-163">Кроме возможности стандартных шаблонов toohello параметров и переменных, hello следующие высокоуровневые конструкции поддерживаются hello шаблона задания:</span><span class="sxs-lookup"><span data-stu-id="21f83-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="21f83-164">**Фабрика задач**</span><span class="sxs-lookup"><span data-stu-id="21f83-164">**Task factory**</span></span>

    -   <span data-ttu-id="21f83-165">Создает несколько задач для одного задания, используя одно определение задачи.</span><span class="sxs-lookup"><span data-stu-id="21f83-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="21f83-166">Поддерживается три типа фабрики задач: параметрический анализ, "по одной задаче на файл" и коллекция задач.</span><span class="sxs-lookup"><span data-stu-id="21f83-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="21f83-167">Hello ниже приведен пример шаблона, который создает задание, которое использует ffmpeg для перекодирования tooone видеофайлов MP4 из низких разрешениях с одной задачи, создаваемых в исходный файл:</span><span class="sxs-lookup"><span data-stu-id="21f83-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
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

<span data-ttu-id="21f83-168">Если файл шаблона hello назывался _ffmpeg.json задания_, то шаблон hello будет вызываться, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="21f83-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="21f83-169">Группы файлов и передача файлов</span><span class="sxs-lookup"><span data-stu-id="21f83-169">File groups and file transfer</span></span>

<span data-ttu-id="21f83-170">Большинство заданий и задач принимают входные файлы и создают выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="21f83-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="21f83-171">Как входные файлы и выходные файлы обычно требуется toobe, переданных из узла toohello hello клиента или от клиента toohello узел hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="21f83-172">Hello Azure CLI пакета расширения абстрагирует передача размещения файлов и использует hello учетной записи хранилища, создаваемый по умолчанию для каждой учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="21f83-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="21f83-173">Файловая группа по алгоритму tooa контейнер, который создается в hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="21f83-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="21f83-174">Hello файловая группа может содержать вложенные папки.</span><span class="sxs-lookup"><span data-stu-id="21f83-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="21f83-175">Hello CLI пакета расширения предоставляет команды для отправки файлов из клиента tooa указанной файловой группе и загрузку файлов из группы tooa hello указанного файла клиента.</span><span class="sxs-lookup"><span data-stu-id="21f83-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="21f83-176">Отключение пула узлы возврат tooa файловой группы или пула и задание шаблоны позволяют файлы, хранящиеся в toobe групп файл, заданный для копирования на узлах пула.</span><span class="sxs-lookup"><span data-stu-id="21f83-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="21f83-177">Например в шаблоне задания, указанный ранее, hello файл группы «ffmpeg-input» указан для hello фабрики задач как hello расположения файлов видео источника hello, записанное на узле hello для перекодирования; Hello файл группы «ffmpeg выход», используются как hello места, где Привет перекодировать выходные файлы скопированы toofrom hello узел под управлением каждой задачи.</span><span class="sxs-lookup"><span data-stu-id="21f83-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="21f83-178">Сводка</span><span class="sxs-lookup"><span data-stu-id="21f83-178">Summary</span></span>

<span data-ttu-id="21f83-179">Шаблон и файл поддержки в данный момент были добавлены только toohello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="21f83-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="21f83-180">Задача Hello — tooexpand hello аудитории, можно использовать toousers пакета, который не обязательно toodevelop кода, с помощью hello пакетных API, например исследователей, ИТ-пользователи и т. д.</span><span class="sxs-lookup"><span data-stu-id="21f83-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="21f83-181">Без кодирования, пользователи, знакомые с Azure, пакета и toobe приложения hello выполнялись пакета можно создавать шаблоны для создания пула и задания.</span><span class="sxs-lookup"><span data-stu-id="21f83-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="21f83-182">С параметрами шаблона пользователи, не зная пакета и hello приложений можно использовать шаблоны hello.</span><span class="sxs-lookup"><span data-stu-id="21f83-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="21f83-183">Испытайте hello пакета расширения для hello Azure CLI, а также получить любые отзывы и предложения, либо в hello комментарии для данной статьи или с помощью hello [форум по пакетной службы Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="21f83-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21f83-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21f83-184">Next steps</span></span>

- <span data-ttu-id="21f83-185">См. hello пакета шаблоны блога: [заданий запущен пакетной службы Azure с помощью hello Azure CLI — код не требуется](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="21f83-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="21f83-186">Подробную документацию по установке и использовании, образцы и исходного кода доступны в hello [репозитории Azure GitHub](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="21f83-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
