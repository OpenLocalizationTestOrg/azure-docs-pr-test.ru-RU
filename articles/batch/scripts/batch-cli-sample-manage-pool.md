---
title: "aaaAzure образец скрипта CLI - Управление пулами в пакете | Документы Microsoft"
description: "Пример скрипта Azure CLI для управления пулами в пакетной службе"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="d51cd-103">Управление пулами пакетной службы Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d51cd-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="d51cd-104">Эти сценарий демонстрирует некоторые hello средства, доступные в Azure CLI toocreate hello и Управление пулами вычислительных узлов в hello пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="d51cd-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="d51cd-105">Hello команды в этом примере создают виртуальные машины Azure.</span><span class="sxs-lookup"><span data-stu-id="d51cd-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="d51cd-106">Работающих виртуальных машин будет начисляется плата за счет tooyour.</span><span class="sxs-lookup"><span data-stu-id="d51cd-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="d51cd-107">После завершения выполнения образца hello toominimize выставления счетов удалить hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d51cd-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="d51cd-108">См. раздел [Очистка пулов](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="d51cd-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="d51cd-109">Пулы пакетной службы можно настроить двумя способами: с помощью настройки облачных служб (только для Windows) или настройки виртуальных машин (для Windows и Linux).</span><span class="sxs-lookup"><span data-stu-id="d51cd-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="d51cd-110">Следующие скрипты образца Hello показывают, как toocreate пулы с обеих конфигураций.</span><span class="sxs-lookup"><span data-stu-id="d51cd-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d51cd-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d51cd-111">Prerequisites</span></span>

- <span data-ttu-id="d51cd-112">Установка hello Azure CLI с помощью hello следуйте инструкциям в hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы еще не выполнена.</span><span class="sxs-lookup"><span data-stu-id="d51cd-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="d51cd-113">Создайте учетную запись пакетной службы, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="d51cd-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="d51cd-114">В разделе [создать пакетную учетную запись с hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) пример сценария, который создает учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d51cd-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="d51cd-115">Настройте toorun приложения из задачи запуска, если это еще не было сделано.</span><span class="sxs-lookup"><span data-stu-id="d51cd-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="d51cd-116">В разделе [Добавление приложений tooAzure пакета с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) приведен пример скрипта, создающий приложение и отправляет tooAzure пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="d51cd-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="d51cd-117">Пример скрипта для пула с настройкой облачной службы</span><span class="sxs-lookup"><span data-stu-id="d51cd-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="d51cd-118">Пример скрипта для пула с настройкой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d51cd-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="d51cd-119">Очистка пулов</span><span class="sxs-lookup"><span data-stu-id="d51cd-119">Clean up pools</span></span>

<span data-ttu-id="d51cd-120">После запуска hello выше образец скрипта запуска hello, следующая команда toodelete hello пулов.</span><span class="sxs-lookup"><span data-stu-id="d51cd-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="d51cd-121">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d51cd-121">Script explanation</span></span>

<span data-ttu-id="d51cd-122">Этот скрипт использует следующие команды toocreate hello и манипулировать пулы пакета.</span><span class="sxs-lookup"><span data-stu-id="d51cd-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="d51cd-123">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="d51cd-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="d51cd-124">Команда</span><span class="sxs-lookup"><span data-stu-id="d51cd-124">Command</span></span> | <span data-ttu-id="d51cd-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="d51cd-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d51cd-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="d51cd-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="d51cd-127">Проверка подлинности учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="d51cd-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="d51cd-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="d51cd-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="d51cd-129">Список доступных приложений hello в hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d51cd-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="d51cd-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="d51cd-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="d51cd-131">Создание пула виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d51cd-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="d51cd-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="d51cd-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="d51cd-133">Обновление свойств пула.</span><span class="sxs-lookup"><span data-stu-id="d51cd-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="d51cd-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="d51cd-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="d51cd-135">Отображение списка доступных номеров SKU агента узла и сведений об образе.</span><span class="sxs-lookup"><span data-stu-id="d51cd-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="d51cd-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="d51cd-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="d51cd-137">Изменение размера hello количество работающих виртуальных машин в hello указано пула.</span><span class="sxs-lookup"><span data-stu-id="d51cd-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="d51cd-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="d51cd-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="d51cd-139">Отображение свойств hello пула.</span><span class="sxs-lookup"><span data-stu-id="d51cd-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="d51cd-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="d51cd-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="d51cd-141">Удалить hello указанного пула.</span><span class="sxs-lookup"><span data-stu-id="d51cd-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="d51cd-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="d51cd-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="d51cd-143">Включение автоматического масштабирования в пуле и применение формулы.</span><span class="sxs-lookup"><span data-stu-id="d51cd-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="d51cd-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="d51cd-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="d51cd-145">Отключение автоматического масштабирования в пуле.</span><span class="sxs-lookup"><span data-stu-id="d51cd-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="d51cd-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="d51cd-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="d51cd-147">Список всех hello вычислительных узлов в hello указанного пула.</span><span class="sxs-lookup"><span data-stu-id="d51cd-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="d51cd-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="d51cd-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="d51cd-149">Перезагрузите hello указанного вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="d51cd-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="d51cd-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="d51cd-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="d51cd-151">Узлы в списке hello Delete из hello указаны пула.</span><span class="sxs-lookup"><span data-stu-id="d51cd-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d51cd-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d51cd-152">Next steps</span></span>

<span data-ttu-id="d51cd-153">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d51cd-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d51cd-154">Дополнительные образцы сценариев CLI пакета можно найти в hello [документации пакета Azure CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d51cd-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

