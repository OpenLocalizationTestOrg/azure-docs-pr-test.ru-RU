---
title: "Пример сценария CLI - aaaAzure шифрования виртуальной Машины Linux | Документы Microsoft"
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
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="fd2ca-103">Шифрование виртуальной машины Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="fd2ca-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="fd2ca-104">Этот сценарий создает безопасное Azure Key Vault, ключи шифрования, субъект-службу Azure Active Directory и виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="fd2ca-105">Hello ВМ шифруется с помощью ключа шифрования hello из хранилища ключей и учетных данных участника службы.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fd2ca-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="fd2ca-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fd2ca-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="fd2ca-107">Clean up deployment</span></span> 

<span data-ttu-id="fd2ca-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fd2ca-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="fd2ca-109">Script explanation</span></span>

<span data-ttu-id="fd2ca-110">Этот скрипт использует следующие команды toocreate hello ресурсов группы, хранилище ключей Azure, служба участника, виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="fd2ca-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fd2ca-112">Команда</span><span class="sxs-lookup"><span data-stu-id="fd2ca-112">Command</span></span> | <span data-ttu-id="fd2ca-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="fd2ca-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd2ca-114">az group create</span><span class="sxs-lookup"><span data-stu-id="fd2ca-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fd2ca-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fd2ca-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="fd2ca-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="fd2ca-117">Создает хранилище ключей Azure toostore безопасности данных, например ключи шифрования.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="fd2ca-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="fd2ca-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="fd2ca-119">Создает ключ шифрования в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="fd2ca-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="fd2ca-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="fd2ca-121">Создает службу Azure Active Directory toosecurely основной проверки подлинности и управления ключами tooencryption доступа.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="fd2ca-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="fd2ca-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="fd2ca-123">Задает разрешения на хранилище ключей toogrant hello разделы tooencryption участнику доступ к службе hello.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="fd2ca-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="fd2ca-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fd2ca-125">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="fd2ca-126">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="fd2ca-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="fd2ca-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="fd2ca-128">Включает шифрование на ВМ с помощью учетных данных участника службы hello и ключ шифрования.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="fd2ca-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="fd2ca-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="fd2ca-130">Показывает состояние hello hello процесс шифрования виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="fd2ca-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="fd2ca-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fd2ca-132">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="fd2ca-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd2ca-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd2ca-133">Next steps</span></span>

<span data-ttu-id="fd2ca-134">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd2ca-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fd2ca-135">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fd2ca-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
