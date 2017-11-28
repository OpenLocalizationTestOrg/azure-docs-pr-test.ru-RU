---
title: "Образец скрипта CLI - выполнении задания с использованием пакета aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI для выполнения задания в пакетной службе."
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="cfd15-103">Выполнение заданий в пакетной службе Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cfd15-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="cfd15-104">Этот скрипт создает пакетного задания и добавляет ряд задач toohello задания.</span><span class="sxs-lookup"><span data-stu-id="cfd15-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="cfd15-105">Он также демонстрирует, как toomonitor задания и его задач.</span><span class="sxs-lookup"><span data-stu-id="cfd15-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="cfd15-106">Наконец он показывает, как tooquery hello пакетная служба эффективно для получения сведений о hello рабочих заданий.</span><span class="sxs-lookup"><span data-stu-id="cfd15-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cfd15-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cfd15-107">Prerequisites</span></span>

- <span data-ttu-id="cfd15-108">Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.</span><span class="sxs-lookup"><span data-stu-id="cfd15-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="cfd15-109">Создайте учетную запись пакетной службы, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="cfd15-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="cfd15-110">В разделе [создать пакетную учетную запись с hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) пример сценария, который создает учетную запись.</span><span class="sxs-lookup"><span data-stu-id="cfd15-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="cfd15-111">Настройте toorun приложения из задачи запуска, если это еще не было сделано.</span><span class="sxs-lookup"><span data-stu-id="cfd15-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="cfd15-112">В разделе [Добавление приложений tooAzure пакета с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) приведен пример скрипта, создающий приложение и отправляет tooAzure пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="cfd15-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="cfd15-113">Настройте пул, на какие hello задание будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="cfd15-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="cfd15-114">Пример скрипта создания пула с использованием конфигурации облачной службы или конфигурации виртуальной машины см. в статье [Управление пулами пакетной службы Azure с помощью Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool).</span><span class="sxs-lookup"><span data-stu-id="cfd15-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="cfd15-115">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="cfd15-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="cfd15-116">Очистка задания</span><span class="sxs-lookup"><span data-stu-id="cfd15-116">Clean up job</span></span>

<span data-ttu-id="cfd15-117">После запуска hello выше образец скрипта запуска hello, следующая команда tooremove задания и всех его задач.</span><span class="sxs-lookup"><span data-stu-id="cfd15-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="cfd15-118">Обратите внимание, что пул hello будет toobe удалена отдельно.</span><span class="sxs-lookup"><span data-stu-id="cfd15-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="cfd15-119">Дополнительные сведения о создании и удалении пулов см. в статье [Управление пулами пакетной службы Azure с помощью Azure CLI](./batch-cli-sample-manage-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cfd15-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="cfd15-120">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="cfd15-120">Script explanation</span></span>

<span data-ttu-id="cfd15-121">Этот скрипт использует следующие команды toocreate hello пакетного задания и задачи.</span><span class="sxs-lookup"><span data-stu-id="cfd15-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="cfd15-122">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="cfd15-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="cfd15-123">Команда</span><span class="sxs-lookup"><span data-stu-id="cfd15-123">Command</span></span> | <span data-ttu-id="cfd15-124">Примечания</span><span class="sxs-lookup"><span data-stu-id="cfd15-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cfd15-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="cfd15-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="cfd15-126">Выполняет аутентификацию учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="cfd15-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="cfd15-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="cfd15-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="cfd15-128">Создает задание пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="cfd15-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="cfd15-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="cfd15-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="cfd15-130">Обновляет свойства задания пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="cfd15-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="cfd15-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="cfd15-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="cfd15-132">Получает сведения об указанном задании пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="cfd15-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="cfd15-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="cfd15-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="cfd15-134">Добавляет toohello задач указан пакетного задания.</span><span class="sxs-lookup"><span data-stu-id="cfd15-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="cfd15-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="cfd15-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="cfd15-136">Извлекает сведения hello задачи из hello указан пакетного задания.</span><span class="sxs-lookup"><span data-stu-id="cfd15-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="cfd15-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="cfd15-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="cfd15-138">Список задач hello, связанный с указанным заданием hello.</span><span class="sxs-lookup"><span data-stu-id="cfd15-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="cfd15-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfd15-139">Next steps</span></span>

<span data-ttu-id="cfd15-140">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cfd15-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cfd15-141">Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cfd15-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
