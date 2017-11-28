---
title: "Пример сценария Azure CLI. Шифрование виртуальной машины Linux | Документация Майкрософт"
description: "Пример сценария Azure CLI для шифрования виртуальной машины Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9388bce04e37d049301521f808cd8494c327e335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="5f7d1-103">Шифрование виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="5f7d1-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="5f7d1-104">Этот сценарий создает безопасное Azure Key Vault, ключи шифрования, субъект-службу Azure Active Directory и виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="5f7d1-105">Затем эта виртуальная машина шифруется с помощью ключа шифрования из Key Vault и учетных данных субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5f7d1-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="5f7d1-106">Sample script</span></span>

<span data-ttu-id="5f7d1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Шифрование дисков виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="5f7d1-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5f7d1-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="5f7d1-108">Clean up deployment</span></span> 

<span data-ttu-id="5f7d1-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5f7d1-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="5f7d1-110">Script explanation</span></span>

<span data-ttu-id="5f7d1-111">Этот сценарий использует приведенные ниже команды для создания группы ресурсов, Azure Key Vault, субъекта-службы, виртуальной машины и всех связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="5f7d1-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5f7d1-113">Команда</span><span class="sxs-lookup"><span data-stu-id="5f7d1-113">Command</span></span> | <span data-ttu-id="5f7d1-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="5f7d1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5f7d1-115">az group create</span><span class="sxs-lookup"><span data-stu-id="5f7d1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5f7d1-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5f7d1-117">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="5f7d1-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="5f7d1-118">Создает Azure Key Vault для хранения защищенных данных, таких как ключи шифрования.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="5f7d1-119">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="5f7d1-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="5f7d1-120">Создает ключ шифрования в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="5f7d1-121">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="5f7d1-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="5f7d1-122">Создает субъект-службу Azure Active Directory для безопасной аутентификации и контроля доступа к ключам шифрования.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="5f7d1-123">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="5f7d1-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="5f7d1-124">Задает разрешения для Key Vault, предоставляя субъекту-службе доступ к ключам шифрования.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="5f7d1-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="5f7d1-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5f7d1-126">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5f7d1-127">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5f7d1-128">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="5f7d1-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="5f7d1-129">Включает шифрование на виртуальной машине с помощью учетных данных субъекта-службы и ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="5f7d1-130">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="5f7d1-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="5f7d1-131">Отображает состояние шифрования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="5f7d1-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="5f7d1-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5f7d1-133">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="5f7d1-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5f7d1-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f7d1-134">Next steps</span></span>

<span data-ttu-id="5f7d1-135">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5f7d1-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5f7d1-136">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f7d1-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
