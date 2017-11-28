---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью виртуального жесткого диска | Документы Майкрософт"
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
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="41263-103">Создание виртуальной машины с помощью виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="41263-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="41263-104">Этот пример создает виртуальную машину с помощью виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="41263-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="41263-105">Он создает группу ресурсов, учетную запись хранение и контейнер, а затем создает виртуальную машину путем отправки виртуального жесткого диска в контейнер.</span><span class="sxs-lookup"><span data-stu-id="41263-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="41263-106">Он заменяет открытый ключ SSH вашим открытым ключом, чтобы предоставить вам доступ к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="41263-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="41263-107">Потребуется загрузочный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="41263-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="41263-108">Можно скачать VHD-диск, который мы использовали, со страницы https://azclisamples.blob.core.windows.net/vhds/sample.vhd или использовать собственный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="41263-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="41263-109">Скрипт ищет `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="41263-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="41263-110">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="41263-110">Sample script</span></span>

<span data-ttu-id="41263-111">[!code-azurecli-interactive[основной](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Создание виртуальной машины с помощью виртуального жесткого диска")]</span><span class="sxs-lookup"><span data-stu-id="41263-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="41263-112">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="41263-112">Clean up deployment</span></span> 

<span data-ttu-id="41263-113">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="41263-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="41263-114">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="41263-114">Script explanation</span></span>

<span data-ttu-id="41263-115">Для создания группы ресурсов, виртуальной машины, группы доступности, балансировщика нагрузки и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="41263-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="41263-116">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="41263-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="41263-117">Команда</span><span class="sxs-lookup"><span data-stu-id="41263-117">Command</span></span> | <span data-ttu-id="41263-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="41263-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41263-119">az group create</span><span class="sxs-lookup"><span data-stu-id="41263-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="41263-120">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="41263-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41263-121">az storage account list</span><span class="sxs-lookup"><span data-stu-id="41263-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="41263-122">Выводит список учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="41263-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="41263-123">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="41263-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="41263-124">Проверяет допустимость имени учетной записи хранения и что она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="41263-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="41263-125">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="41263-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="41263-126">Выводит список ключей для учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="41263-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="41263-127">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="41263-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="41263-128">Проверяет, существует ли BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="41263-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="41263-129">az storage container create</span><span class="sxs-lookup"><span data-stu-id="41263-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="41263-130">Создает контейнер в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="41263-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="41263-131">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="41263-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="41263-132">Создает BLOB-объект в контейнере путем отправки виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="41263-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="41263-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="41263-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="41263-134">Используется с `--query`, чтобы проверить, используется ли имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="41263-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="41263-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="41263-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="41263-136">Создает виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="41263-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="41263-137">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="41263-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="41263-138">Сбрасывает ключ SSH для предоставления текущему пользователю прав доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="41263-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="41263-139">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="41263-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="41263-140">Возвращает IP-адрес созданной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="41263-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41263-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41263-141">Next steps</span></span>

<span data-ttu-id="41263-142">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41263-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="41263-143">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="41263-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
