---
title: "Пример сценария CLI - aaaAzure создать узел Docker | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание узла Docker"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="167a7-103">Создание виртуальной машины с помощью Docker</span><span class="sxs-lookup"><span data-stu-id="167a7-103">Create a VM with Docker</span></span>

<span data-ttu-id="167a7-104">Этот сценарий создает виртуальную машину с включенным Docker и запускает контейнер Docker, в котором будет запущен NGINX.</span><span class="sxs-lookup"><span data-stu-id="167a7-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="167a7-105">После выполнения сценария hello, можно обращаться из веб-сервер NGINX hello hello полное доменное имя виртуальной машины Azure hello.</span><span class="sxs-lookup"><span data-stu-id="167a7-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="167a7-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="167a7-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="167a7-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="167a7-107">Clean up deployment</span></span> 

<span data-ttu-id="167a7-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="167a7-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="167a7-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="167a7-109">Script explanation</span></span>

<span data-ttu-id="167a7-110">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="167a7-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="167a7-111">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="167a7-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="167a7-112">Команда</span><span class="sxs-lookup"><span data-stu-id="167a7-112">Command</span></span> | <span data-ttu-id="167a7-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="167a7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="167a7-114">az group create</span><span class="sxs-lookup"><span data-stu-id="167a7-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="167a7-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="167a7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="167a7-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="167a7-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="167a7-117">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="167a7-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="167a7-118">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="167a7-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="167a7-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="167a7-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="167a7-120">Создает tooallow правило группы безопасности сети входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="167a7-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="167a7-121">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="167a7-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="167a7-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="167a7-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="167a7-123">Добавляет и запускает tooa расширения виртуальной машины виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="167a7-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="167a7-124">В этом образце hello расширение ВМ Docker является используется tooconfigure узел Docker.</span><span class="sxs-lookup"><span data-stu-id="167a7-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="167a7-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="167a7-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="167a7-126">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="167a7-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="167a7-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="167a7-127">Next steps</span></span>

<span data-ttu-id="167a7-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="167a7-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="167a7-129">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="167a7-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
