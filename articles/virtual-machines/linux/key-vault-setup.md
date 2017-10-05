---
title: "Настройка Azure Key Vault для виртуальных машин Linux | Документация Майкрософт"
description: "Как настроить Key Vault для использования с виртуальной машиной Azure Resource Manager c помощью интерфейса командной строки 2.0."
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
ms.openlocfilehash: 2cc9b4c978e9a4deb0c8443c4b0f9e301a7cf492
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="25cd1-103">Как настроить Key Vault для виртуальных машин с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="25cd1-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="25cd1-104">В стеке Azure Resource Manager секреты и сертификаты представляют собой ресурсы, которые предоставляются Key Vault.</span><span class="sxs-lookup"><span data-stu-id="25cd1-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="25cd1-105">Чтобы больше узнать о хранилище ключей Azure, ознакомьтесь с разделом [Что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="25cd1-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="25cd1-106">Чтобы Key Vault можно было использовать для виртуальных машин Azure Resource Manager, свойству *EnabledForDeployment* в Key Vault должно быть присвоено значение true.</span><span class="sxs-lookup"><span data-stu-id="25cd1-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="25cd1-107">В этой статье показано, как настроить Key Vault для использования с виртуальными машинами Azure с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="25cd1-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="25cd1-108">Эти действия можно также выполнить с помощью [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="25cd1-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="25cd1-109">Чтобы выполнить эти действия, нужно установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="25cd1-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="25cd1-110">создать хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="25cd1-110">Create a Key Vault</span></span>
<span data-ttu-id="25cd1-111">Создайте Key Vault и назначьте политику развертывания с помощью команды [az keyvault create](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="25cd1-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="25cd1-112">В следующем примере создается Key Vault `myKeyVault` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="25cd1-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="25cd1-113">Обновление Key Vault для использования с виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="25cd1-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="25cd1-114">Установите политику развертывания в существующем Key Vault с помощью команды [az keyvault update](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="25cd1-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="25cd1-115">В следующем примере обновляется Key Vault `myKeyVault` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="25cd1-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="25cd1-116">Использование шаблонов для настройки хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="25cd1-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="25cd1-117">При использовании шаблона свойству `enabledForDeployment` ресурса Key Vault нужно присвоить значение `true`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="25cd1-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="25cd1-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25cd1-118">Next steps</span></span>
<span data-ttu-id="25cd1-119">Сведения о других параметрах, которые можно настроить при создании Key Vault с помощью шаблонов, см. в разделе [Create a Key Vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/) (Создание Key Vault).</span><span class="sxs-lookup"><span data-stu-id="25cd1-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
