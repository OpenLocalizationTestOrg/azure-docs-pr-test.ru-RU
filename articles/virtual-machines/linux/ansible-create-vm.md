---
title: "Использование Ansible для создания базовой виртуальной машины Linux в Azure | Документы Майкрософт"
description: "Узнайте, как использовать Ansible для создания базовой виртуальной машины Linux в Azure и управления ею."
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="ccce8-103">Создание базовой виртуальной машины в Azure с помощью Ansible</span><span class="sxs-lookup"><span data-stu-id="ccce8-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="ccce8-104">Ansible позволяет автоматизировать развертывание и настройку ресурсов в среде.</span><span class="sxs-lookup"><span data-stu-id="ccce8-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="ccce8-105">Ansible можно использовать для управления виртуальными машинами в Azure так же, как любым другим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="ccce8-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="ccce8-106">В этой статье показано, как создать базовую виртуальную машину с помощью Ansible.</span><span class="sxs-lookup"><span data-stu-id="ccce8-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="ccce8-107">Вы также можете узнать, как [создать готовую среду виртуальных машин с помощью Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ccce8-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ccce8-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ccce8-108">Prerequisites</span></span>
<span data-ttu-id="ccce8-109">Для управления ресурсами Azure с помощью Ansible необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="ccce8-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="ccce8-110">Ansible и модули SDK Python для Azure, установленные в системе узла.</span><span class="sxs-lookup"><span data-stu-id="ccce8-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="ccce8-111">Ansible можно установить в [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) и [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).</span><span class="sxs-lookup"><span data-stu-id="ccce8-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="ccce8-112">Учетные данные Azure, настроенные для использования в Ansible.</span><span class="sxs-lookup"><span data-stu-id="ccce8-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="ccce8-113">Создание учетных данных Azure и настройка Ansible</span><span class="sxs-lookup"><span data-stu-id="ccce8-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="ccce8-114">Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ccce8-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ccce8-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="ccce8-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="ccce8-116">Если вам необходимо выполнить обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ccce8-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="ccce8-117">Вы также можете использовать [Cloud Shell](/azure/cloud-shell/quickstart) из своего браузера.</span><span class="sxs-lookup"><span data-stu-id="ccce8-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="ccce8-118">Создание вспомогательных ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ccce8-118">Create supporting Azure resources</span></span>
<span data-ttu-id="ccce8-119">В этом примере мы создадим модуль runbook, который развертывает виртуальную машину в существующей инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="ccce8-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="ccce8-120">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="ccce8-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="ccce8-121">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="ccce8-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ccce8-122">Создайте виртуальную сеть для виртуальной машины с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="ccce8-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="ccce8-123">В следующем примере создаются виртуальная сеть *myVnet* и подсеть *mySubnet*.</span><span class="sxs-lookup"><span data-stu-id="ccce8-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="ccce8-124">Создание и запуск скрипта playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="ccce8-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="ccce8-125">Создайте скрипт playbook Ansible с именем **azure_create_vm.yml** и вставьте приведенное ниже содержимое.</span><span class="sxs-lookup"><span data-stu-id="ccce8-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="ccce8-126">В этом примере создается одна виртуальная машина и настраиваются учетные данные SSH.</span><span class="sxs-lookup"><span data-stu-id="ccce8-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="ccce8-127">Введите собственные данные открытого ключа в паре *key_data* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ccce8-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

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

<span data-ttu-id="ccce8-128">Чтобы создать виртуальную машину с помощью Ansible, запустите скрипт playbook следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ccce8-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="ccce8-129">Ниже приведен пример выходных данных, в котором показано, что виртуальная машина успешно создана:</span><span class="sxs-lookup"><span data-stu-id="ccce8-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="ccce8-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ccce8-130">Next steps</span></span>
<span data-ttu-id="ccce8-131">В этом примере создается виртуальная машина в существующей группе ресурсов с уже развернутой виртуальной сетью.</span><span class="sxs-lookup"><span data-stu-id="ccce8-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="ccce8-132">Более подробный пример использования Ansible для создания вспомогательных ресурсов, таких как виртуальная сеть и правила группы безопасности сети, см. в статье [Создание готовой среды виртуальных машин с помощью Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ccce8-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>