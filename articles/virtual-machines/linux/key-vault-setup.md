---
title: "aaaSet копирование хранилища ключей Azure для виртуальных машин Linux | Документы Microsoft"
description: "Как tooset копии хранилища ключей для использования в виртуальной машине Azure Resource Manager с hello CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="0b61a-103">Как tooset копию ключа хранилища для виртуальных машин с hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0b61a-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="0b61a-104">В стеке диспетчера ресурсов Azure hello секреты или сертификаты моделируются в виде ресурсов, предоставляемых хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="0b61a-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="0b61a-105">toolearn Дополнительные сведения о хранилище ключей Azure, в разделе [что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0b61a-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="0b61a-106">Чтобы использовать с виртуальными машинами Azure Resource Manager toobe хранилище ключей, hello *EnabledForDeployment* свойства хранилища ключей должен быть указан tootrue.</span><span class="sxs-lookup"><span data-stu-id="0b61a-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="0b61a-107">В этой статье рассказывается, как tooset копии хранилища ключей для использования с виртуальными машинами Azure (ВМ) с помощью hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0b61a-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="0b61a-108">Можно также выполнить следующие действия с hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b61a-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0b61a-109">tooperform эти шаги, необходимые hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0b61a-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="0b61a-110">создать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="0b61a-110">Create a Key Vault</span></span>
<span data-ttu-id="0b61a-111">Создание хранилища ключей и назначение политики развертывания hello с [az keyvault создать](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="0b61a-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="0b61a-112">Hello следующий пример создает хранилища ключей с именем `myKeyVault` в hello `myResourceGroup` группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="0b61a-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="0b61a-113">Обновление Key Vault для использования с виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="0b61a-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="0b61a-114">Задать политику развертывания hello в существующем хранилище ключей с [обновление keyvault az](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="0b61a-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="0b61a-115">Hello следующие обновления hello хранилища ключей с именем `myKeyVault` в hello `myResourceGroup` группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="0b61a-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="0b61a-116">Используйте шаблоны tooset копии хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0b61a-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="0b61a-117">При использовании шаблона необходимо tooset hello `enabledForDeployment` свойство слишком`true` для ресурса хранилища ключей hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0b61a-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0b61a-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b61a-118">Next steps</span></span>
<span data-ttu-id="0b61a-119">Сведения о других параметрах, которые можно настроить при создании Key Vault с помощью шаблонов, см. в разделе [Create a Key Vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/) (Создание Key Vault).</span><span class="sxs-lookup"><span data-stu-id="0b61a-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
