---
title: "Пример скрипта Azure CLI для управления пулами в пакетной службе | Документация Майкрософт"
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="7a2f8-103">Управление пулами пакетной службы Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7a2f8-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="7a2f8-104">Этот скрипт демонстрирует некоторые из доступных средств Azure CLI для создания пулов вычислительных узлов в пакетной службе Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="7a2f8-105">В этом примере используются команды для создания виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="7a2f8-106">При использовании виртуальных машин с вашей учетной записи будет взиматься плата.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="7a2f8-107">Чтобы свести к минимуму эти расходы, удалите виртуальные машины, когда завершите использование примера.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="7a2f8-108">См. раздел [Очистка пулов](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="7a2f8-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="7a2f8-109">Пулы пакетной службы можно настроить двумя способами: с помощью настройки облачных служб (только для Windows) или настройки виртуальных машин (для Windows и Linux).</span><span class="sxs-lookup"><span data-stu-id="7a2f8-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="7a2f8-110">В примерах скриптов ниже показано, как создать пулы с использованием этих двух конфигураций.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a2f8-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7a2f8-111">Prerequisites</span></span>

- <span data-ttu-id="7a2f8-112">Установите Azure CLI с помощью инструкций, приведенных в [руководстве по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="7a2f8-113">Создайте учетную запись пакетной службы, если у вас ее еще нет.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="7a2f8-114">Пример скрипта создания учетной записи см. в статье [Создание учетной записи пакетной службы с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account).</span><span class="sxs-lookup"><span data-stu-id="7a2f8-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="7a2f8-115">Настройте выполнение приложения из задачи запуска, если вы этого еще не сделали.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="7a2f8-116">Пример скрипта создания приложения и отправки пакета приложения в Azure см. в статье [Добавление приложений в пакетную службу Azure с помощью Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application).</span><span class="sxs-lookup"><span data-stu-id="7a2f8-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="7a2f8-117">Пример скрипта для пула с настройкой облачной службы</span><span class="sxs-lookup"><span data-stu-id="7a2f8-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="7a2f8-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Управление пулами облачных служб")]</span><span class="sxs-lookup"><span data-stu-id="7a2f8-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="7a2f8-119">Пример скрипта для пула с настройкой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7a2f8-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="7a2f8-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Управление пулами виртуальных машин")]</span><span class="sxs-lookup"><span data-stu-id="7a2f8-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="7a2f8-121">Очистка пулов</span><span class="sxs-lookup"><span data-stu-id="7a2f8-121">Clean up pools</span></span>

<span data-ttu-id="7a2f8-122">После выполнения представленного выше примера скрипта запустите следующую команду, чтобы удалить пулы.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="7a2f8-123">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="7a2f8-123">Script explanation</span></span>

<span data-ttu-id="7a2f8-124">Для создания и обработки пулов пакетной службы этот скрипт использует указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="7a2f8-125">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7a2f8-126">Команда</span><span class="sxs-lookup"><span data-stu-id="7a2f8-126">Command</span></span> | <span data-ttu-id="7a2f8-127">Примечания</span><span class="sxs-lookup"><span data-stu-id="7a2f8-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a2f8-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="7a2f8-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="7a2f8-129">Проверка подлинности учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="7a2f8-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="7a2f8-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="7a2f8-131">Список доступных приложений в учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="7a2f8-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="7a2f8-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="7a2f8-133">Создание пула виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="7a2f8-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="7a2f8-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="7a2f8-135">Обновление свойств пула.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="7a2f8-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="7a2f8-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="7a2f8-137">Отображение списка доступных номеров SKU агента узла и сведений об образе.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="7a2f8-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="7a2f8-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="7a2f8-139">Изменение количества работающих виртуальных машин в указанном пуле.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="7a2f8-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="7a2f8-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="7a2f8-141">Отображение свойств пула.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="7a2f8-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="7a2f8-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="7a2f8-143">Удаление указанного пула.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="7a2f8-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="7a2f8-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="7a2f8-145">Включение автоматического масштабирования в пуле и применение формулы.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="7a2f8-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="7a2f8-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="7a2f8-147">Отключение автоматического масштабирования в пуле.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="7a2f8-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="7a2f8-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="7a2f8-149">Отображение списка всех вычислительных узлов в указанном пуле.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="7a2f8-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="7a2f8-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="7a2f8-151">Перезагрузка указанного вычислительного узла.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="7a2f8-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="7a2f8-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="7a2f8-153">Удаление указанных узлов из указанного пула.</span><span class="sxs-lookup"><span data-stu-id="7a2f8-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="7a2f8-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7a2f8-154">Next steps</span></span>

<span data-ttu-id="7a2f8-155">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a2f8-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a2f8-156">Дополнительные примеры скриптов для интерфейса командной строки пакетной службы см. в [документации по интерфейсу командной строки пакетной службы Azure](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7a2f8-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

