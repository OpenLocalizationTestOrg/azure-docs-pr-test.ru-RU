---
title: "aaaAzure образец скрипта CLI - перезапустить виртуальные машины | Документы Microsoft"
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
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="378be-103">Перезапуск виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="378be-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="378be-104">В этом примере показано два способа tooget некоторые виртуальные машины и перезапустить их.</span><span class="sxs-lookup"><span data-stu-id="378be-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="378be-105">Сначала Hello перезапускает все виртуальные машины hello в группе ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="378be-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="378be-106">Hello второй возвращает hello тегом виртуальных машин с помощью `az resouce list` фильтрует toohello ресурсы, которые являются виртуальными машинами и перезапускает этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="378be-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="378be-107">Этот пример работает в оболочке Bash.</span><span class="sxs-lookup"><span data-stu-id="378be-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="378be-108">Параметры запуска на клиенте Windows Azure CLI скриптов см [работающих в Windows Azure CLI hello](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="378be-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="378be-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="378be-109">Sample script</span></span>

<span data-ttu-id="378be-110">Образец Hello имеет три сценарии.</span><span class="sxs-lookup"><span data-stu-id="378be-110">hello sample has three scripts.</span></span>
<span data-ttu-id="378be-111">Здравствуйте, первый из них обеспечивать hello виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="378be-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="378be-112">Он использует параметр ожидания нет hello, поэтому команда hello возвращается без ожидания на каждой виртуальной Машины, toobe подготовлены.</span><span class="sxs-lookup"><span data-stu-id="378be-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="378be-113">Во-вторых Hello ожидает полной подготовки toobe ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="378be-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="378be-114">Третий сценарий Hello перезапускает все виртуальные машины hello, которые были подготовлены, а затем просто hello тегами для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="378be-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="378be-115">Hello подготовки виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="378be-115">Provision hello VMs</span></span>

<span data-ttu-id="378be-116">Этот скрипт создает группу ресурсов, а затем он создает toorestart три виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="378be-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="378be-117">Две из них имеют теги.</span><span class="sxs-lookup"><span data-stu-id="378be-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="378be-118">Ожидание</span><span class="sxs-lookup"><span data-stu-id="378be-118">Wait</span></span>

<span data-ttu-id="378be-119">Этот сценарий проверяет состояние подготовки каждые 20 секунд, пока все три виртуальных машин или один из них происходит сбой tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="378be-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="378be-120">Перезапустите hello виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="378be-120">Restart hello VMs</span></span>

<span data-ttu-id="378be-121">Этот сценарий перезапускает все виртуальные машины hello в группе ресурсов hello и перезапускает только виртуальные машины с тегами hello.</span><span class="sxs-lookup"><span data-stu-id="378be-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="378be-122">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="378be-122">Clean up deployment</span></span> 

<span data-ttu-id="378be-123">После выполнения сценария образец hello hello, следующая команда может быть групп ресурсов используется tooremove hello, виртуальные машины и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="378be-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="378be-124">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="378be-124">Script explanation</span></span>

<span data-ttu-id="378be-125">Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="378be-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="378be-126">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="378be-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="378be-127">Команда</span><span class="sxs-lookup"><span data-stu-id="378be-127">Command</span></span> | <span data-ttu-id="378be-128">Примечания</span><span class="sxs-lookup"><span data-stu-id="378be-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="378be-129">az group create</span><span class="sxs-lookup"><span data-stu-id="378be-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="378be-130">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="378be-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="378be-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="378be-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="378be-132">Создает hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="378be-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="378be-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="378be-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="378be-134">При использовании `--query` hello tooensure виртуальных машин, подготавливаются перед перезапуском их, а затем tooget hello идентификаторы toorestart hello виртуальных машин их.</span><span class="sxs-lookup"><span data-stu-id="378be-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="378be-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="378be-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="378be-136">При использовании `--query` tooget hello идентификаторы hello виртуальных машин с помощью тега hello.</span><span class="sxs-lookup"><span data-stu-id="378be-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="378be-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="378be-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="378be-138">Перезапускает ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="378be-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="378be-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="378be-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="378be-140">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="378be-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="378be-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="378be-141">Next steps</span></span>

<span data-ttu-id="378be-142">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="378be-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="378be-143">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="378be-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
