---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины Linux с NGINX | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="9db32-103">Создание виртуальной машины с помощью NGINX</span><span class="sxs-lookup"><span data-stu-id="9db32-103">Create a VM with NGINX</span></span>

<span data-ttu-id="9db32-104">Этот скрипт создает виртуальную машину Azure и использует виртуальную машину Azure настраиваемое расширение скриптов hello tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="9db32-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="9db32-105">После выполнения сценария hello, можно получить доступ к демонстрационной веб-сайта на общедоступный IP-адрес hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9db32-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9db32-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9db32-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="9db32-107">Расширение пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="9db32-107">Custom Script Extension</span></span>

<span data-ttu-id="9db32-108">расширение пользовательского скрипта Hello копирует этот скрипт на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="9db32-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="9db32-109">сценарий Hello запустите tooinstall и настроить веб-сервер NGINX.</span><span class="sxs-lookup"><span data-stu-id="9db32-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="9db32-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="9db32-110">Clean up deployment</span></span> 

<span data-ttu-id="9db32-111">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="9db32-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9db32-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="9db32-112">Script explanation</span></span>

<span data-ttu-id="9db32-113">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9db32-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9db32-114">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="9db32-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9db32-115">Команда</span><span class="sxs-lookup"><span data-stu-id="9db32-115">Command</span></span> | <span data-ttu-id="9db32-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="9db32-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9db32-117">az group create</span><span class="sxs-lookup"><span data-stu-id="9db32-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9db32-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9db32-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9db32-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="9db32-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9db32-120">Создает виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="9db32-120">Creates hello virtual machine.</span></span> <span data-ttu-id="9db32-121">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="9db32-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9db32-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="9db32-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="9db32-123">Создает tooallow правило группы безопасности сети входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="9db32-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="9db32-124">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="9db32-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="9db32-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="9db32-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9db32-126">Добавляет и запускает tooa расширения виртуальной машины виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9db32-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="9db32-127">В этом образце hello расширение пользовательского скрипта является используется tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="9db32-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="9db32-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="9db32-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9db32-129">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="9db32-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9db32-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9db32-130">Next steps</span></span>

<span data-ttu-id="9db32-131">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9db32-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9db32-132">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9db32-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
