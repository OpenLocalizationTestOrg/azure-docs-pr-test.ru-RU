---
title: "Пример сценария CLI - aaaAzure развертывание hello стек LAMP в Load-Balanced виртуальную компьюте Мя_входа наборе масштабирования | Документы Microsoft"
description: "Использовать пользовательский сценарий расширения toodeploy hello стек LAMP загрузки = сбалансированная масштабирования виртуальных машин на Azure."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="b59aa-103">Развертывание стек LAMP hello в наборе масштабирования виртуальных машин с балансировкой нагрузки</span><span class="sxs-lookup"><span data-stu-id="b59aa-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="b59aa-104">В этом примере создается набор масштабирования виртуальной машины и применяет расширение, работающей на каждую виртуальную машину в наборе масштабирования hello стек LAMP hello toodeploy пользовательского скрипта.</span><span class="sxs-lookup"><span data-stu-id="b59aa-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="b59aa-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="b59aa-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="b59aa-106">Подключение</span><span class="sxs-lookup"><span data-stu-id="b59aa-106">Connect</span></span>

<span data-ttu-id="b59aa-107">Используйте этот код toosee, как задать tooconnect tooyour виртуальных машин и масштаба.</span><span class="sxs-lookup"><span data-stu-id="b59aa-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b59aa-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="b59aa-108">Clean up deployment</span></span> 

<span data-ttu-id="b59aa-109">Запустите следующие группы ресурсов hello tooremove команд, hello набор масштабирования и виртуальные машины и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="b59aa-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b59aa-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="b59aa-110">Script explanation</span></span>

<span data-ttu-id="b59aa-111">Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b59aa-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="b59aa-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="b59aa-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b59aa-113">Команда</span><span class="sxs-lookup"><span data-stu-id="b59aa-113">Command</span></span> | <span data-ttu-id="b59aa-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="b59aa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b59aa-115">az group create</span><span class="sxs-lookup"><span data-stu-id="b59aa-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b59aa-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b59aa-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b59aa-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="b59aa-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="b59aa-118">Создает масштабируемый набор виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b59aa-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="b59aa-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="b59aa-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="b59aa-120">Добавляет конечную точку с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b59aa-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="b59aa-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="b59aa-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="b59aa-122">Создание расширения hello, выполняет пользовательский скрипт hello развертывания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b59aa-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="b59aa-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="b59aa-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="b59aa-124">Проведение hello экземпляров виртуальных Машин, которые были развернуты до применения hello расширение пользовательского скрипта hello toohello набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="b59aa-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="b59aa-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="b59aa-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="b59aa-126">Вертикальное масштабирование шкалы hello, задать, добавив дополнительные экземпляры виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b59aa-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="b59aa-127">Hello пользовательского скрипта выполняется на их при развертывании.</span><span class="sxs-lookup"><span data-stu-id="b59aa-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="b59aa-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="b59aa-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="b59aa-129">Получение IP-адреса hello hello виртуальные машины, созданные в образце hello.</span><span class="sxs-lookup"><span data-stu-id="b59aa-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="b59aa-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="b59aa-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="b59aa-131">Получение hello внешнего и внутреннего порты, используемые подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="b59aa-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b59aa-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b59aa-132">Next steps</span></span>

<span data-ttu-id="b59aa-133">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b59aa-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b59aa-134">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b59aa-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
