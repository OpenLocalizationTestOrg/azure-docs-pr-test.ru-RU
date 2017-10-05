---
title: "Пример сценария Azure CLI для выполнения задания с помощью пакетной службы | Документация Майкрософт"
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="d557d-103">Выполнение заданий в пакетной службе Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d557d-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="d557d-104">Этот сценарий создает задание пакетной службы и добавляет в него ряд задач.</span><span class="sxs-lookup"><span data-stu-id="d557d-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="d557d-105">Он также демонстрирует, как отслеживать задание и его задачи.</span><span class="sxs-lookup"><span data-stu-id="d557d-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="d557d-106">Кроме того, он показывает, как эффективно выполнять запрос к пакетной службе на получение сведений о задачах задания.</span><span class="sxs-lookup"><span data-stu-id="d557d-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d557d-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d557d-107">Prerequisites</span></span>

- <span data-ttu-id="d557d-108">Установите Azure CLI с помощью инструкций, приведенных в [руководстве по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="d557d-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="d557d-109">Создайте учетную запись пакетной службы, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="d557d-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="d557d-110">Пример скрипта создания учетной записи см. в статье [Создание учетной записи пакетной службы с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account).</span><span class="sxs-lookup"><span data-stu-id="d557d-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="d557d-111">Настройте выполнение приложения из задачи запуска, если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="d557d-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="d557d-112">Пример скрипта создания приложения и отправки пакета приложения в Azure см. в статье [Добавление приложений в пакетную службу Azure с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application).</span><span class="sxs-lookup"><span data-stu-id="d557d-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="d557d-113">Настройте пул, в котором будет выполняться задание.</span><span class="sxs-lookup"><span data-stu-id="d557d-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="d557d-114">Пример скрипта создания пула с использованием конфигурации облачной службы или конфигурации виртуальной машины см. в статье [Управление пулами пакетной службы Azure с помощью Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool).</span><span class="sxs-lookup"><span data-stu-id="d557d-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d557d-115">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d557d-115">Sample script</span></span>

<span data-ttu-id="d557d-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Выполнение задания")]</span><span class="sxs-lookup"><span data-stu-id="d557d-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="d557d-117">Очистка задания</span><span class="sxs-lookup"><span data-stu-id="d557d-117">Clean up job</span></span>

<span data-ttu-id="d557d-118">После выполнения представленного выше примера сценария выполните следующую команду, чтобы удалить задание и все его задачи.</span><span class="sxs-lookup"><span data-stu-id="d557d-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="d557d-119">Обратите внимание, что пул нужно удалить отдельно.</span><span class="sxs-lookup"><span data-stu-id="d557d-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="d557d-120">Дополнительные сведения о создании и удалении пулов см. в статье [Управление пулами пакетной службы Azure с помощью Azure CLI](./batch-cli-sample-manage-pool.md).</span><span class="sxs-lookup"><span data-stu-id="d557d-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="d557d-121">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d557d-121">Script explanation</span></span>

<span data-ttu-id="d557d-122">Чтобы создать задание и задачи пакетной службы, сценарий использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d557d-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="d557d-123">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d557d-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d557d-124">Команда</span><span class="sxs-lookup"><span data-stu-id="d557d-124">Command</span></span> | <span data-ttu-id="d557d-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="d557d-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d557d-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="d557d-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="d557d-127">Выполняет аутентификацию учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d557d-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="d557d-128">az batch job create</span><span class="sxs-lookup"><span data-stu-id="d557d-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="d557d-129">Создает задание пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d557d-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="d557d-130">az batch job set</span><span class="sxs-lookup"><span data-stu-id="d557d-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="d557d-131">Обновляет свойства задания пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d557d-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="d557d-132">az batch job show</span><span class="sxs-lookup"><span data-stu-id="d557d-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="d557d-133">Получает сведения об указанном задании пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d557d-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="d557d-134">az batch task create</span><span class="sxs-lookup"><span data-stu-id="d557d-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="d557d-135">Добавляет задачу в указанное задание пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d557d-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="d557d-136">az batch task show</span><span class="sxs-lookup"><span data-stu-id="d557d-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="d557d-137">Получает сведения о задаче из указанного задания пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d557d-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="d557d-138">az batch task list</span><span class="sxs-lookup"><span data-stu-id="d557d-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="d557d-139">Выводит список задач, связанных с определенным заданием.</span><span class="sxs-lookup"><span data-stu-id="d557d-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d557d-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d557d-140">Next steps</span></span>

<span data-ttu-id="d557d-141">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d557d-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d557d-142">Дополнительные примеры скриптов для интерфейса командной строки пакетной службы см. в [документации по интерфейсу командной строки пакетной службы Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d557d-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
