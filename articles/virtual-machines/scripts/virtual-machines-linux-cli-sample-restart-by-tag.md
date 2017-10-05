---
title: "Пример сценария Azure CLI. Перезапуск виртуальных машин | Документация Майкрософт"
description: "Пример сценария Azure CLI. Перезапуск виртуальных машин с использованием тега и идентификатора"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: 4d0fe95287c91a4b656904f9007ceaaf866e155f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="restart-vms"></a><span data-ttu-id="3fadf-103">Перезапуск виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="3fadf-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="3fadf-104">В этом примере показано несколько способов получить несколько виртуальных машин и перезапустить их.</span><span class="sxs-lookup"><span data-stu-id="3fadf-104">This sample shows a couple of ways to get some VMs and restart them.</span></span>

<span data-ttu-id="3fadf-105">Первый пример перезапускает все виртуальные машины в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3fadf-105">The first restarts all the VMs in the resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="3fadf-106">Второй возвращает виртуальные машины с тегами с помощью команды `az resouce list`, применяет фильтр, оставляя только те ресурсы, которые являются виртуальными машинами, и перезапускает их.</span><span class="sxs-lookup"><span data-stu-id="3fadf-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="3fadf-107">Этот пример работает в оболочке Bash.</span><span class="sxs-lookup"><span data-stu-id="3fadf-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="3fadf-108">Сведения о параметрах выполнения скриптов Azure CLI в клиенте Windows см. в статье [Использование Azure CLI в Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="3fadf-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="3fadf-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="3fadf-109">Sample script</span></span>

<span data-ttu-id="3fadf-110">Пример состоит из трех сценариев.</span><span class="sxs-lookup"><span data-stu-id="3fadf-110">The sample has three scripts.</span></span>
<span data-ttu-id="3fadf-111">Первый подготавливает виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="3fadf-111">The first one provisions the virtual machines.</span></span>
<span data-ttu-id="3fadf-112">В нем используется параметр no-wait, поэтому команда возвращается без ожидания подготовки каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3fadf-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span></span>
<span data-ttu-id="3fadf-113">Второй ожидает, пока виртуальные машины не будут полностью подготовлены.</span><span class="sxs-lookup"><span data-stu-id="3fadf-113">The second waits for the VMs to be fully provisioned.</span></span>
<span data-ttu-id="3fadf-114">Третий сценарий перезапускает все виртуальные машины, которые были подготовлены, и затем — только виртуальные машины с тегами.</span><span class="sxs-lookup"><span data-stu-id="3fadf-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span></span>

### <a name="provision-the-vms"></a><span data-ttu-id="3fadf-115">Подготовка виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="3fadf-115">Provision the VMs</span></span>

<span data-ttu-id="3fadf-116">Этот сценарий создает группу ресурсов и создает три виртуальные машины, которые следует перезапустить.</span><span class="sxs-lookup"><span data-stu-id="3fadf-116">This script creates a resource group and then it creates three VMs to restart.</span></span>
<span data-ttu-id="3fadf-117">Две из них имеют теги.</span><span class="sxs-lookup"><span data-stu-id="3fadf-117">Two of them are tagged.</span></span>

<span data-ttu-id="3fadf-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Подготовка виртуальных машин")]</span><span class="sxs-lookup"><span data-stu-id="3fadf-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]</span></span>

### <a name="wait"></a><span data-ttu-id="3fadf-119">Ожидание</span><span class="sxs-lookup"><span data-stu-id="3fadf-119">Wait</span></span>

<span data-ttu-id="3fadf-120">Этот сценарий проверяет состояние подготовки каждые 20 секунд, пока все три виртуальные машины не будут подготовлены или подготовка одной из них не завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="3fadf-120">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span></span>

<span data-ttu-id="3fadf-121">[!code-azurecli-interactive[основной](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Ожидание подготовки виртуальных машин")]</span><span class="sxs-lookup"><span data-stu-id="3fadf-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]</span></span>

### <a name="restart-the-vms"></a><span data-ttu-id="3fadf-122">Перезапуск виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="3fadf-122">Restart the VMs</span></span>

<span data-ttu-id="3fadf-123">Этот сценарий перезапускает все виртуальные машины в группе ресурсов, а затем перезапускает только виртуальные машины с тегами.</span><span class="sxs-lookup"><span data-stu-id="3fadf-123">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span></span>

<span data-ttu-id="3fadf-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Перезапуск виртуальных машин с использованием тега")]</span><span class="sxs-lookup"><span data-stu-id="3fadf-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3fadf-125">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="3fadf-125">Clean up deployment</span></span> 

<span data-ttu-id="3fadf-126">После выполнения примера сценария можно удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3fadf-126">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="3fadf-127">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="3fadf-127">Script explanation</span></span>

<span data-ttu-id="3fadf-128">Для создания группы ресурсов, виртуальной машины, группы доступности, балансировщика нагрузки и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="3fadf-128">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="3fadf-129">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="3fadf-129">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3fadf-130">Команда</span><span class="sxs-lookup"><span data-stu-id="3fadf-130">Command</span></span> | <span data-ttu-id="3fadf-131">Примечания</span><span class="sxs-lookup"><span data-stu-id="3fadf-131">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3fadf-132">az group create</span><span class="sxs-lookup"><span data-stu-id="3fadf-132">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3fadf-133">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3fadf-133">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3fadf-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="3fadf-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="3fadf-135">Создает виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="3fadf-135">Creates the virtual machines.</span></span>  |
| [<span data-ttu-id="3fadf-136">az vm list</span><span class="sxs-lookup"><span data-stu-id="3fadf-136">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="3fadf-137">Используется с `--query`, чтобы обеспечить подготовку виртуальных машин, прежде чем они будут перезапущены, а затем — чтобы получить идентификаторы виртуальных машин для их перезапуска.</span><span class="sxs-lookup"><span data-stu-id="3fadf-137">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span></span> |
| [<span data-ttu-id="3fadf-138">az resource list</span><span class="sxs-lookup"><span data-stu-id="3fadf-138">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="3fadf-139">Используется с `--query` для получения идентификаторов виртуальных машин по тегу.</span><span class="sxs-lookup"><span data-stu-id="3fadf-139">Used with `--query` to get the IDs of the VMs using the tag.</span></span> |
| [<span data-ttu-id="3fadf-140">az vm restart</span><span class="sxs-lookup"><span data-stu-id="3fadf-140">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="3fadf-141">Перезагружает виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="3fadf-141">Restarts the VMs.</span></span> |
| [<span data-ttu-id="3fadf-142">az group delete</span><span class="sxs-lookup"><span data-stu-id="3fadf-142">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3fadf-143">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="3fadf-143">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3fadf-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3fadf-144">Next steps</span></span>

<span data-ttu-id="3fadf-145">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3fadf-145">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3fadf-146">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3fadf-146">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
