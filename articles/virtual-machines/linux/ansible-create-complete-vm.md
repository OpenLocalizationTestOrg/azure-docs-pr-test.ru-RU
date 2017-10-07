---
title: "toocreate Ansible aaaUse завершения виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Узнайте, как toouse Ansible toocreate и управления ими полную среду виртуальных машин Linux в Azure"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="8ab3f-103">Создание готовой среды виртуальных машин Linux в Azure с помощью Ansible</span><span class="sxs-lookup"><span data-stu-id="8ab3f-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="8ab3f-104">Ansible позволяет tooautomate hello развертывание и настройку ресурсов в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="8ab3f-105">Можно использовать виртуальные машины (VM) Ansible toomanage в Azure, hello таким же, как и любой другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="8ab3f-106">В этой статье показано, как toocreate полную среду Linux и поддержку ресурсов с Ansible.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="8ab3f-107">Также вы можете узнать, каким образом слишком[Создание базовых ВМ с Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="8ab3f-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8ab3f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8ab3f-108">Prerequisites</span></span>
<span data-ttu-id="8ab3f-109">toomanage Azure ресурсы с Ansible необходимо hello следующие:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="8ab3f-110">Ansible и hello в системе узла установлены модули Azure Python SDK.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="8ab3f-111">Ansible можно установить в [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) и [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).</span><span class="sxs-lookup"><span data-stu-id="8ab3f-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="8ab3f-112">Учетные данные Azure и toouse Ansible настроить их.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="8ab3f-113">Создание учетных данных Azure и настройка Ansible</span><span class="sxs-lookup"><span data-stu-id="8ab3f-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="8ab3f-114">Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8ab3f-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="8ab3f-116">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8ab3f-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="8ab3f-117">Вы также можете использовать [Cloud Shell](/azure/cloud-shell/quickstart) из своего браузера.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="8ab3f-118">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="8ab3f-118">Create virtual network</span></span>
<span data-ttu-id="8ab3f-119">Hello следующий раздел в репертуара Ansible создает виртуальную сеть с именем *myVnet* в hello *10.0.0.0/16* пространства адресов:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="8ab3f-120">tooadd подсети hello в следующем разделе создает подсеть с именем *mySubnet* в hello *myVnet* виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="8ab3f-121">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="8ab3f-121">Create public IP address</span></span>
<span data-ttu-id="8ab3f-122">tooaccess ресурсам через Интернет, hello создайте и назначьте открытый IP адрес tooyour виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="8ab3f-123">Hello следующий раздел в репертуара Ansible создает общедоступный IP-адрес с именем *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="8ab3f-124">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="8ab3f-124">Create Network Security Group</span></span>
<span data-ttu-id="8ab3f-125">Hello поток сетевого трафика и из него ВМ управления группами безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="8ab3f-126">Hello следующий раздел в репертуара Ansible создает группу безопасности сети с именем *myNetworkSecurityGroup* и определяет правило tooallow SSH трафик на TCP-порт 22:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="8ab3f-127">Создание виртуальных сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="8ab3f-127">Create virtual network interface card</span></span>
<span data-ttu-id="8ab3f-128">Виртуальный сетевой адаптер (NIC) подключается tooa вашей виртуальной Машины, заданного виртуальной сети, общедоступный IP-адрес и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="8ab3f-129">Hello следующий раздел в репертуара Ansible создает виртуальный сетевой Адаптер с именем *myNIC* toohello виртуальных сетевых ресурсов вы создали подключение:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="8ab3f-130">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8ab3f-130">Create virtual machine</span></span>
<span data-ttu-id="8ab3f-131">Последний шаг Hello представляет собой виртуальную Машину toocreate и использовать все ресурсы hello, созданные.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="8ab3f-132">Hello следующий раздел в репертуара Ansible создает Виртуальную машину с именем *myVM* и присоединяет hello виртуальный сетевой Адаптер с именем *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="8ab3f-133">Введите свои собственные данные открытого ключа в hello *key_data* пары следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="8ab3f-134">Завершение скрипта playbook Ansible</span><span class="sxs-lookup"><span data-stu-id="8ab3f-134">Complete Ansible playbook</span></span>
<span data-ttu-id="8ab3f-135">toobring в этих разделах, создающим репертуара Ansible с именем *azure_create_complete_vm.yml* и вставить hello содержимое:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="8ab3f-136">Ansible должен toodeploy группы ресурсов, все ресурсы в.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="8ab3f-137">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="8ab3f-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="8ab3f-138">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8ab3f-139">toocreate hello полную ВМ среду с Ansible, запустите репертуара hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="8ab3f-140">Hello выходные данные выглядят аналогично toohello следующий пример, показывающий hello успешность создания виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="8ab3f-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="8ab3f-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8ab3f-141">Next steps</span></span>
<span data-ttu-id="8ab3f-142">Этот пример создает полную среду виртуальной Машины, включая hello необходимых виртуальных сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8ab3f-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="8ab3f-143">Более прямой toocreate примере ВМ в существующих сетевых ресурсов с параметрами по умолчанию. в разделе [создания виртуальной Машины](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="8ab3f-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
