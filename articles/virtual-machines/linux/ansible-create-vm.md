---
title: "toocreate Ansible aaaUse основные виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Узнайте, как toouse Ansible toocreate и управления ими основные виртуальной машины Linux в Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="a41b1-103">Создание базовой виртуальной машины в Azure с помощью Ansible</span><span class="sxs-lookup"><span data-stu-id="a41b1-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="a41b1-104">Ansible позволяет tooautomate hello развертывание и настройку ресурсов в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="a41b1-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="a41b1-105">Можно использовать виртуальные машины (VM) Ansible toomanage в Azure, hello таким же, как и любой другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="a41b1-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="a41b1-106">В этой статье показано, как toocreate основные виртуальной Машины с Ansible.</span><span class="sxs-lookup"><span data-stu-id="a41b1-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="a41b1-107">Также вы можете узнать, каким образом слишком[создать полную среду виртуальной Машины с Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a41b1-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a41b1-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a41b1-108">Prerequisites</span></span>
<span data-ttu-id="a41b1-109">toomanage Azure ресурсы с Ansible необходимо hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a41b1-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="a41b1-110">Ansible и hello в системе узла установлены модули Azure Python SDK.</span><span class="sxs-lookup"><span data-stu-id="a41b1-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="a41b1-111">Ansible можно установить в [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) и [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).</span><span class="sxs-lookup"><span data-stu-id="a41b1-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="a41b1-112">Учетные данные Azure и toouse Ansible настроить их.</span><span class="sxs-lookup"><span data-stu-id="a41b1-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="a41b1-113">Создание учетных данных Azure и настройка Ansible</span><span class="sxs-lookup"><span data-stu-id="a41b1-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="a41b1-114">Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a41b1-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a41b1-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="a41b1-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="a41b1-116">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a41b1-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a41b1-117">Вы также можете использовать [Cloud Shell](/azure/cloud-shell/quickstart) из своего браузера.</span><span class="sxs-lookup"><span data-stu-id="a41b1-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="a41b1-118">Создание вспомогательных ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a41b1-118">Create supporting Azure resources</span></span>
<span data-ttu-id="a41b1-119">В этом примере мы создадим модуль runbook, который развертывает виртуальную машину в существующей инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="a41b1-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="a41b1-120">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a41b1-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a41b1-121">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="a41b1-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a41b1-122">Создайте виртуальную сеть для виртуальной машины с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="a41b1-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="a41b1-123">Hello следующий пример создает виртуальную сеть с именем *myVnet* и подсеть с именем *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a41b1-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="a41b1-124">Создание и запуск скрипта playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="a41b1-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="a41b1-125">Создание репертуара Ansible с именем **azure_create_vm.yml** и hello вставить содержимое.</span><span class="sxs-lookup"><span data-stu-id="a41b1-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="a41b1-126">В этом примере создается одна виртуальная машина и настраиваются учетные данные SSH.</span><span class="sxs-lookup"><span data-stu-id="a41b1-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="a41b1-127">Введите свои собственные данные открытого ключа в hello *key_data* пары следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a41b1-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="a41b1-128">hello toocreate виртуальную Машину с Ansible, запустите репертуара hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a41b1-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="a41b1-129">Hello выходные данные выглядят аналогично toohello следующий пример, показывающий hello успешность создания виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="a41b1-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="a41b1-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a41b1-130">Next steps</span></span>
<span data-ttu-id="a41b1-131">В этом примере создается виртуальная машина в существующей группе ресурсов с уже развернутой виртуальной сетью.</span><span class="sxs-lookup"><span data-stu-id="a41b1-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="a41b1-132">Более подробный пример о том, как toouse Ansible toocreate вспомогательные ресурсы о виртуальной сети и правила группы безопасности сети, в разделе [создать полную среду виртуальной Машины с Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a41b1-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
