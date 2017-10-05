---
title: "Повторное развертывание виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Повторное развертывание виртуальных машин Linux в Azure для устранения проблем подключения по протоколу SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 7a8653a82775e718c38f65f246d997ba61f99d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="5694a-103">Повторное развертывание виртуальной машины Linux на новом узле Azure</span><span class="sxs-lookup"><span data-stu-id="5694a-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="5694a-104">Если у вас возникли сложности при устранении неполадок подключения SSH или получения доступа к приложению на виртуальной машине Linux в Azure, можно попробовать повторно развернуть виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="5694a-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="5694a-105">При повторном развертывании виртуальная машина перемещается на новый узел в рамках инфраструктуры Azure, где она повторно включается.</span><span class="sxs-lookup"><span data-stu-id="5694a-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="5694a-106">При этом сохраняются все параметры конфигурации и связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="5694a-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="5694a-107">В этой статье показано, как повторно развернуть виртуальную машину с помощью интерфейса командной строки Azure или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5694a-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5694a-108">После развертывания временный диск будет удален, а связанные с виртуальным сетевым интерфейсом динамические IP-адреса будут обновлены.</span><span class="sxs-lookup"><span data-stu-id="5694a-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="5694a-109">Можно повторно развернуть виртуальную машину с помощью одного из приведенных способов.</span><span class="sxs-lookup"><span data-stu-id="5694a-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="5694a-110">Необходимо выбрать один из вариантов для повторного развертывания виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="5694a-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="5694a-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5694a-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="5694a-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5694a-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="5694a-113">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5694a-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="5694a-114">Использование Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5694a-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="5694a-115">Установите последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войдите в систему с учетной записью Azure, выполнив команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5694a-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="5694a-116">Повторно разверните виртуальную машину, выполнив команду [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="5694a-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="5694a-117">В следующем примере повторно развертывается виртуальная машина с именем *myVM*, входящая в группу ресурсов с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5694a-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="5694a-118">Использование Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5694a-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="5694a-119">Установите [последнюю версию Azure CLI 1.0](../../cli-install-nodejs.md), войдите в систему с учетной записью Azure и убедитесь, что используется режим Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="5694a-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="5694a-120">В следующем примере повторно развертывается виртуальная машина с именем *myVM*, входящая в группу ресурсов с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="5694a-120">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="5694a-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5694a-121">Next steps</span></span>
<span data-ttu-id="5694a-122">При проблемах с подключением к виртуальной машине ознакомьтесь со статьями [Устранение неполадок SSH-подключения к виртуальной машине Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) и [Подробное описание устранения неполадок SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5694a-122">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5694a-123">При проблемах с доступом к приложению, выполняющемуся в виртуальной машине, ознакомьтесь со статьей [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5694a-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

