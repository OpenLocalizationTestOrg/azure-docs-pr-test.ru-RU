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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Создание готовой среды виртуальных машин Linux в Azure с помощью Ansible
Ansible позволяет tooautomate hello развертывание и настройку ресурсов в вашей среде. Можно использовать виртуальные машины (VM) Ansible toomanage в Azure, hello таким же, как и любой другой ресурс. В этой статье показано, как toocreate полную среду Linux и поддержку ресурсов с Ansible. Также вы можете узнать, каким образом слишком[Создание базовых ВМ с Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Предварительные требования
toomanage Azure ресурсы с Ansible необходимо hello следующие:

- Ansible и hello в системе узла установлены модули Azure Python SDK.
    - Ansible можно установить в [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) и [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).
- Учетные данные Azure и toouse Ansible настроить их.
    - [Создание учетных данных Azure и настройка Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI версии 2.0.4 или более поздней. Запустите `az --version` версии toofind hello. 
    - Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). Вы также можете использовать [Cloud Shell](/azure/cloud-shell/quickstart) из своего браузера.


## <a name="create-virtual-network"></a>Создание виртуальной сети
Hello следующий раздел в репертуара Ansible создает виртуальную сеть с именем *myVnet* в hello *10.0.0.0/16* пространства адресов:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd подсети hello в следующем разделе создает подсеть с именем *mySubnet* в hello *myVnet* виртуальной сети:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Создание общедоступного IP-адреса
tooaccess ресурсам через Интернет, hello создайте и назначьте открытый IP адрес tooyour виртуальной Машины. Hello следующий раздел в репертуара Ansible создает общедоступный IP-адрес с именем *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Создание группы безопасности сети
Hello поток сетевого трафика и из него ВМ управления группами безопасности сети. Hello следующий раздел в репертуара Ansible создает группу безопасности сети с именем *myNetworkSecurityGroup* и определяет правило tooallow SSH трафик на TCP-порт 22:

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


## <a name="create-virtual-network-interface-card"></a>Создание виртуальных сетевых адаптеров
Виртуальный сетевой адаптер (NIC) подключается tooa вашей виртуальной Машины, заданного виртуальной сети, общедоступный IP-адрес и группы безопасности сети. Hello следующий раздел в репертуара Ansible создает виртуальный сетевой Адаптер с именем *myNIC* toohello виртуальных сетевых ресурсов вы создали подключение:

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


## <a name="create-virtual-machine"></a>Создание виртуальной машины
Последний шаг Hello представляет собой виртуальную Машину toocreate и использовать все ресурсы hello, созданные. Hello следующий раздел в репертуара Ansible создает Виртуальную машину с именем *myVM* и присоединяет hello виртуальный сетевой Адаптер с именем *myNIC*. Введите свои собственные данные открытого ключа в hello *key_data* пары следующим образом:

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

## <a name="complete-ansible-playbook"></a>Завершение скрипта playbook Ansible
toobring в этих разделах, создающим репертуара Ansible с именем *azure_create_complete_vm.yml* и вставить hello содержимое:

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

Ansible должен toodeploy группы ресурсов, все ресурсы в. Создайте группу ресурсов с помощью команды [az group create](/cli/azure/vm#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello полную ВМ среду с Ansible, запустите репертуара hello следующим образом:

```bash
ansible-playbook azure_create_complete_vm.yml
```

Hello выходные данные выглядят аналогично toohello следующий пример, показывающий hello успешность создания виртуальной Машины:

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

## <a name="next-steps"></a>Дальнейшие действия
Этот пример создает полную среду виртуальной Машины, включая hello необходимых виртуальных сетевых ресурсов. Более прямой toocreate примере ВМ в существующих сетевых ресурсов с параметрами по умолчанию. в разделе [создания виртуальной Машины](ansible-create-vm.md).
