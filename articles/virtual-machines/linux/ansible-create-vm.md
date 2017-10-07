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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Создание базовой виртуальной машины в Azure с помощью Ansible
Ansible позволяет tooautomate hello развертывание и настройку ресурсов в вашей среде. Можно использовать виртуальные машины (VM) Ansible toomanage в Azure, hello таким же, как и любой другой ресурс. В этой статье показано, как toocreate основные виртуальной Машины с Ansible. Также вы можете узнать, каким образом слишком[создать полную среду виртуальной Машины с Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Предварительные требования
toomanage Azure ресурсы с Ansible необходимо hello следующие:

- Ansible и hello в системе узла установлены модули Azure Python SDK.
    - Ansible можно установить в [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) и [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2).
- Учетные данные Azure и toouse Ansible настроить их.
    - [Создание учетных данных Azure и настройка Ansible](ansible-install-configure.md#create-azure-credentials)
- Azure CLI версии 2.0.4 или более поздней. Запустите `az --version` версии toofind hello. 
    - Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). Вы также можете использовать [Cloud Shell](/azure/cloud-shell/quickstart) из своего браузера.


## <a name="create-supporting-azure-resources"></a>Создание вспомогательных ресурсов Azure
В этом примере мы создадим модуль runbook, который развертывает виртуальную машину в существующей инфраструктуре. Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/vm#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroup --location eastus
```

Создайте виртуальную сеть для виртуальной машины с помощью команды [az network vnet create](/cli/azure/network/vnet#create). Hello следующий пример создает виртуальную сеть с именем *myVnet* и подсеть с именем *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Создание и запуск скрипта playbook Ansible
Создание репертуара Ansible с именем **azure_create_vm.yml** и hello вставить содержимое. В этом примере создается одна виртуальная машина и настраиваются учетные данные SSH. Введите свои собственные данные открытого ключа в hello *key_data* пары следующим образом:

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

hello toocreate виртуальную Машину с Ansible, запустите репертуара hello следующим образом:

```bash
ansible-playbook azure_create_vm.yml
```

Hello выходные данные выглядят аналогично toohello следующий пример, показывающий hello успешность создания виртуальной Машины:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Дальнейшие действия
В этом примере создается виртуальная машина в существующей группе ресурсов с уже развернутой виртуальной сетью. Более подробный пример о том, как toouse Ansible toocreate вспомогательные ресурсы о виртуальной сети и правила группы безопасности сети, в разделе [создать полную среду виртуальной Машины с Ansible](ansible-create-complete-vm.md).
