---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью NGINX | Документация Майкрософт"
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
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="ad998-103">Создание виртуальной машины с помощью NGINX</span><span class="sxs-lookup"><span data-stu-id="ad998-103">Create a VM with NGINX</span></span>

<span data-ttu-id="ad998-104">Этот сценарий создает виртуальную машину в Azure, а затем использует расширение пользовательских сценариев для виртуальных машин Azure, чтобы установить NGINX.</span><span class="sxs-lookup"><span data-stu-id="ad998-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="ad998-105">После выполнения сценария можно получить доступ к веб-сайту с демоверсиями по общедоступному IP-адресу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ad998-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ad998-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ad998-106">Sample script</span></span>

<span data-ttu-id="ad998-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Быстрое создание виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="ad998-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="ad998-108">Расширение пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="ad998-108">Custom Script Extension</span></span>

<span data-ttu-id="ad998-109">Расширение пользовательских скриптов копирует этот скрипт на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ad998-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="ad998-110">Затем скрипт выполняется для установки и настройки веб-сервера NGINX.</span><span class="sxs-lookup"><span data-stu-id="ad998-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="ad998-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ad998-111">Clean up deployment</span></span> 

<span data-ttu-id="ad998-112">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ad998-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ad998-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ad998-113">Script explanation</span></span>

<span data-ttu-id="ad998-114">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ad998-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="ad998-115">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="ad998-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ad998-116">Команда</span><span class="sxs-lookup"><span data-stu-id="ad998-116">Command</span></span> | <span data-ttu-id="ad998-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="ad998-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ad998-118">az group create</span><span class="sxs-lookup"><span data-stu-id="ad998-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ad998-119">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ad998-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ad998-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="ad998-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ad998-121">Создает виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ad998-121">Creates the virtual machine.</span></span> <span data-ttu-id="ad998-122">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="ad998-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ad998-123">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="ad998-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="ad998-124">Создает правило группы безопасности сети, разрешающее входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="ad998-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="ad998-125">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="ad998-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="ad998-126">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="ad998-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ad998-127">Добавляет расширение виртуальной машины в виртуальную машину и выполняет его.</span><span class="sxs-lookup"><span data-stu-id="ad998-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="ad998-128">В этом примере для установки NGINX используется расширение пользовательских скриптов.</span><span class="sxs-lookup"><span data-stu-id="ad998-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="ad998-129">az group delete</span><span class="sxs-lookup"><span data-stu-id="ad998-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ad998-130">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="ad998-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ad998-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad998-131">Next steps</span></span>

<span data-ttu-id="ad998-132">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad998-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ad998-133">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad998-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
