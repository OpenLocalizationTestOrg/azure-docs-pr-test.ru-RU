---
title: "Пример сценария CLI - aaaAzure Создание ВМ с виртуального жесткого диска | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины с помощью виртуального жесткого диска."
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="04e97-103">Создание виртуальной машины с помощью виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="04e97-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="04e97-104">Этот пример создает виртуальную машину с помощью виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="04e97-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="04e97-105">Он создает группу ресурсов, учетной записи хранилища и контейнер, а затем создает виртуальную Машину путем загрузки контейнера toohello hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="04e97-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="04e97-106">Он заменяет hello ssh открытого ключа с помощью открытого ключа, чтобы получить доступ toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="04e97-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="04e97-107">Потребуется загрузочный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="04e97-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="04e97-108">Можно загрузить VHD, который мы использовали hello https://azclisamples.blob.core.windows.net/vhds/sample.vhd или использовать собственный VHD-ФАЙЛ.</span><span class="sxs-lookup"><span data-stu-id="04e97-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="04e97-109">ищет скрипт Hello `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="04e97-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="04e97-110">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="04e97-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="04e97-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="04e97-111">Clean up deployment</span></span> 

<span data-ttu-id="04e97-112">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="04e97-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="04e97-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="04e97-113">Script explanation</span></span>

<span data-ttu-id="04e97-114">Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="04e97-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="04e97-115">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="04e97-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="04e97-116">Команда</span><span class="sxs-lookup"><span data-stu-id="04e97-116">Command</span></span> | <span data-ttu-id="04e97-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="04e97-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="04e97-118">az group create</span><span class="sxs-lookup"><span data-stu-id="04e97-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="04e97-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="04e97-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="04e97-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="04e97-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="04e97-121">Выводит список учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="04e97-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="04e97-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="04e97-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="04e97-123">Проверяет допустимость имени учетной записи хранения и что она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="04e97-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="04e97-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="04e97-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="04e97-125">Выводит список ключей для учетных записей хранения hello</span><span class="sxs-lookup"><span data-stu-id="04e97-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="04e97-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="04e97-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="04e97-127">Проверяет, существует ли hello больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="04e97-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="04e97-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="04e97-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="04e97-129">Создает контейнер в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="04e97-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="04e97-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="04e97-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="04e97-131">Создает большой двоичный объект в контейнере hello, отправка hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="04e97-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="04e97-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="04e97-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="04e97-133">При использовании `--query` проверки, является ли имя виртуальной Машины hello используется.</span><span class="sxs-lookup"><span data-stu-id="04e97-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="04e97-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="04e97-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="04e97-135">Создает hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="04e97-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="04e97-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="04e97-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="04e97-137">Сбрасывает hello SSH ключа toogive hello текущий пользователь доступ toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="04e97-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="04e97-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="04e97-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="04e97-139">Получает IP-адрес hello hello виртуальной Машины, который был создан.</span><span class="sxs-lookup"><span data-stu-id="04e97-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="04e97-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04e97-140">Next steps</span></span>

<span data-ttu-id="04e97-141">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04e97-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="04e97-142">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04e97-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
