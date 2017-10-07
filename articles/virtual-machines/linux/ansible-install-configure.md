---
title: "aaaInstall и настроить для использования с виртуальными машинами Azure Ansible | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить для управления ресурсами Azure на Ubuntu CentOS и SLES Ansible"
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
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Установка и настройка Ansible toomanage виртуальных машин в Azure
В этой статье указаны hello как tooinstall Ansible и необходимые модули Azure Python SDK, для некоторых типичных дистрибутивы Linux. Можно установить Ansible на других дистрибутивах перемещая hello установлены пакеты toofit вашей конкретной платформы. toocreate Azure ресурсы в безопасном режиме, вы также узнаете, как toocreate и укажите учетные данные для Ansible toouse. 

Дополнительные параметры установки и шаги для дополнительных платформ см. в разделе hello [Ansible руководство по установке](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Установка Ansible
Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает группу ресурсов с именем *myResourceGroupAnsible* в hello *eastus* расположение:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Теперь создайте виртуальную Машину и установите Ansible для одного из следующих дистрибутивы hello.

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` нижеприведенного hello операции создания вывод hello виртуальной Машины:

```bash
ssh azureuser@<publicIpAddress>
```

На ВМ установите hello необходимые пакеты для модулей Azure Python SDK hello и Ansible следующим образом:

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

Теперь перейдем слишком[учетные данные Azure создать](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` нижеприведенного hello операции создания вывод hello виртуальной Машины:

```bash
ssh azureuser@<publicIpAddress>
```

На ВМ установите hello необходимые пакеты для модулей Azure Python SDK hello и Ansible следующим образом:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Теперь перейдем слишком[учетные данные Azure создать](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). Hello следующий пример создает Виртуальную машину с именем *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` нижеприведенного hello операции создания вывод hello виртуальной Машины:

```bash
ssh azureuser@<publicIpAddress>
```

На ВМ установите hello необходимые пакеты для модулей Azure Python SDK hello и Ansible следующим образом:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Теперь перейдем слишком[учетные данные Azure создать](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Создание учетных данных Azure
Ansible взаимодействует с Azure, используя имя пользователя и пароль или субъект-службу. Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Ansible. Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure. безопасность tooimprove просто задать имя пользователя и пароль, этот пример создает базовую службу участника.

Создание службы с основной [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и hello учетные данные, которые требуется Ansible выходные данные:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Пример выходных данных hello hello предшествующий команды выглядит следующим образом:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure, необходимо также идентификатор подписки Azure с tooobtain [az учетной записи, отображают](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

В следующем шаге hello используйте hello выходные данные этих двух команд.


## <a name="create-ansible-credentials-file"></a>Создание файла учетных данных Ansible
tooprovide учетные данные tooAnsible, определения переменных среды или создать файл локальные учетные данные. Дополнительные сведения о том, как toodefine Ansible учетные данные, в разделе [tooAzure учетные данные, предоставляя модулей](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

В среде разработки создайте файл *учетных данных* для Ansible в виртуальной машине узла следующим образом:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Hello *учетные данные* сам файл объединяет hello идентификатор подписки с выводом hello создания участника службы. Выходные данные предыдущей hello [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) команда является таким же hello заказа, необходимые для *client_id*, *секрет*, и *клиента* . Следующий пример Hello *учетные данные* файле отображаются эти значения соответствия hello предыдущие выходные данные. Введите свои значения следующим образом:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Использование переменных среды Ansible
Если вы собираетесь toouse средств, таких как Ansible Tower или Jenkins, переменные среды можно определить следующим образом. Эти переменные объединять hello идентификатор подписки с результатом hello создания участника службы. Выходные данные предыдущей hello [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) команда является таким же hello заказа, необходимые для *AZURE_CLIENT_ID*, *AZURE_SECRET*, и *AZURE_ КЛИЕНТ*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь у вас есть Ansible и hello необходимые модули Azure Python SDK, а учетные данные, определенные для Ansible toouse. Узнайте, каким образом слишком[Создание ВМ с Ansible](ansible-create-vm.md). Также вы можете узнать, каким образом слишком[создания завершения виртуальной Машины Azure и поддержку ресурсов с Ansible](ansible-create-complete-vm.md).
