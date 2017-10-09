---
title: "aaaCreate виртуальной Машины Linux в Azure из шаблона | Документы Microsoft"
description: "Как toouse hello Azure CLI 2.0 toocreate ВМ Linux на основе шаблона диспетчера ресурсов"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="57532-103">Как toocreate виртуальной машины Linux с помощью шаблонов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="57532-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="57532-104">В этой статье показано, как tooquickly развертывание виртуальной машины (VM) Linux с помощью шаблонов диспетчера ресурсов Azure и Azure CLI 2.0 hello.</span><span class="sxs-lookup"><span data-stu-id="57532-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="57532-105">Можно также выполнить следующие действия с hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="57532-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="57532-106">Обзор шаблонов</span><span class="sxs-lookup"><span data-stu-id="57532-106">Templates overview</span></span>
<span data-ttu-id="57532-107">Шаблоны Azure Resource Manager являются файлов JSON, которые определяют hello инфраструктурой и настройкой решение Azure.</span><span class="sxs-lookup"><span data-stu-id="57532-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="57532-108">Этот шаблон можно использовать, чтобы повторно развертывать решение на протяжении всего его жизненного цикла и гарантировать, что ресурсы развертываются в согласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="57532-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="57532-109">toolearn Дополнительные сведения о формате hello hello шаблона и при создании, в разделе [создать свой первый диспетчера ресурсов Azure](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="57532-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="57532-110">hello tooview синтаксис JSON для типов ресурсов, в разделе [определения ресурсов в шаблоны Azure Resource Manager](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="57532-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="57532-111">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="57532-111">Create resource group</span></span>
<span data-ttu-id="57532-112">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="57532-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="57532-113">Группу ресурсов следует создавать до виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="57532-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="57532-114">Hello следующий пример создает группу ресурсов с именем *myResourceGroupVM* в hello *eastus* область:</span><span class="sxs-lookup"><span data-stu-id="57532-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="57532-115">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="57532-115">Create virtual machine</span></span>
<span data-ttu-id="57532-116">Hello следующий пример создает виртуальную Машину [этого шаблона Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) с [создания развертывания группы az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="57532-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="57532-117">Укажите значение hello собственный открытый ключ SSH, такие как содержимое hello *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="57532-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="57532-118">Если вам требуется toocreate пару ключей SSH, см. раздел [как toocreate и использование SSH пары ключей для виртуальных машин Linux в Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="57532-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="57532-119">В этом примере указан шаблон, хранящийся в GitHub.</span><span class="sxs-lookup"><span data-stu-id="57532-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="57532-120">Можно также загрузить или создать шаблон и укажите локальный путь hello с hello же `--template-file` параметра.</span><span class="sxs-lookup"><span data-stu-id="57532-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="57532-121">tooSSH tooyour виртуальной Машины, получить hello общедоступный IP-адрес с [az сети public-ip show](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="57532-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="57532-122">Затем вы сможете tooyour SSH виртуальной Машины в обычном режиме:</span><span class="sxs-lookup"><span data-stu-id="57532-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="57532-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57532-123">Next steps</span></span>
<span data-ttu-id="57532-124">В этом примере вы создали базовую виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="57532-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="57532-125">Дополнительные шаблоны диспетчера ресурсов, включающие платформы приложений или создавать более сложные среды, Обзор hello [коллекции шаблонов Azure краткое руководство](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="57532-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
