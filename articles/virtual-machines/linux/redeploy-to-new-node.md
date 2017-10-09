---
title: "aaaRedeploy виртуальных машин Linux в Azure | Документы Microsoft"
description: "Как проблемы tooredeploy виртуальных машин Linux в Azure toomitigate SSH-подключения."
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
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="97377-103">Повторное развертывание виртуальной машины Linux toonew узла Azure</span><span class="sxs-lookup"><span data-stu-id="97377-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="97377-104">Если сталкиваются с трудностями, устранение неполадок SSH или приложений доступа к tooa Linux виртуальной машины (VM) в Azure, повторное развертывание hello виртуальной Машины может помочь.</span><span class="sxs-lookup"><span data-stu-id="97377-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="97377-105">При повторном развертывании виртуальной Машины, перемещает hello ВМ tooa новый узел в рамках hello инфраструктуры Azure и затем включаются.</span><span class="sxs-lookup"><span data-stu-id="97377-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="97377-106">При этом сохраняются все параметры конфигурации и связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="97377-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="97377-107">В этой статье показано, как tooredeploy в виртуальную Машину с помощью Azure CLI или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="97377-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="97377-108">После повторного развертывания виртуальной Машины, теряется временный диск hello и обновляются динамические IP-адреса, связанные с виртуального сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="97377-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="97377-109">Можно повторно развернуть ВМ с помощью одного из следующих вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="97377-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="97377-110">Требуется только один параметр tooredeploy toochoose ВМ:</span><span class="sxs-lookup"><span data-stu-id="97377-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="97377-111">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="97377-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="97377-112">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="97377-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="97377-113">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="97377-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="97377-114">Использовать hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="97377-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="97377-115">Последняя версия hello установки [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="97377-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="97377-116">Повторно разверните виртуальную машину, выполнив команду [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="97377-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="97377-117">Следующий пример повторно развертывает Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="97377-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="97377-118">Использовать hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="97377-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="97377-119">Установка hello [последние Azure CLI 1.0](../../cli-install-nodejs.md), войдите в учетную запись Azure tooan и убедитесь, что вы находитесь в режиме диспетчера ресурсов (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="97377-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="97377-120">Следующий пример повторно развертывает Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="97377-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="97377-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97377-121">Next steps</span></span>
<span data-ttu-id="97377-122">Если возникли проблемы с подключением tooyour виртуальной Машины, можно найти справку на [Устранение неполадок соединений по протоколу SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или [подробные шаги по устранению неполадок SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97377-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="97377-123">При проблемах с доступом к приложению, выполняющемуся в виртуальной машине, ознакомьтесь со статьей [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97377-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

