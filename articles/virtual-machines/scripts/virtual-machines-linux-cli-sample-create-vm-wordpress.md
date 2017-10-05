---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью WordPress | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью WordPress"
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
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="ebefc-103">Создание виртуальной машины с помощью WordPress</span><span class="sxs-lookup"><span data-stu-id="ebefc-103">Create a VM with WordPress</span></span>

<span data-ttu-id="ebefc-104">Этот скрипт создает виртуальную машину, а затем использует расширение пользовательских скриптов виртуальной машины Azure для установки WordPress.</span><span class="sxs-lookup"><span data-stu-id="ebefc-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="ebefc-105">После выполнения сценария можно получить доступ к сайту конфигурации WordPress по адресу `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="ebefc-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ebefc-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="ebefc-106">Sample script</span></span>

<span data-ttu-id="ebefc-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Быстрое создание виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="ebefc-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ebefc-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="ebefc-108">Clean up deployment</span></span> 

<span data-ttu-id="ebefc-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ebefc-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ebefc-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="ebefc-110">Script explanation</span></span>

<span data-ttu-id="ebefc-111">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="ebefc-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="ebefc-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="ebefc-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ebefc-113">Команда</span><span class="sxs-lookup"><span data-stu-id="ebefc-113">Command</span></span> | <span data-ttu-id="ebefc-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="ebefc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ebefc-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ebefc-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ebefc-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ebefc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ebefc-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="ebefc-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ebefc-118">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="ebefc-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="ebefc-119">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="ebefc-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ebefc-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="ebefc-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="ebefc-121">Создает правило группы безопасности сети, разрешающее входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="ebefc-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="ebefc-122">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="ebefc-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="ebefc-123">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="ebefc-123">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ebefc-124">Добавляет расширение пользовательских скриптов на виртуальную машину, вызывающее скрипт для установки WordPress.</span><span class="sxs-lookup"><span data-stu-id="ebefc-124">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
| [<span data-ttu-id="ebefc-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="ebefc-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ebefc-126">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="ebefc-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ebefc-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ebefc-127">Next steps</span></span>

<span data-ttu-id="ebefc-128">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ebefc-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ebefc-129">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ebefc-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
