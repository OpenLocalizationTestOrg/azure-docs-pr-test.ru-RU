---
title: "Установка и настройка Ansible для использования с виртуальными машинами Azure | Документы Майкрософт"
description: "Узнайте, как установить и настроить Ansible для управления ресурсами Azure в Ubuntu, CentOS и SLES."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: jeconnoc
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/18/2017
ms.author: iainfou
ms.openlocfilehash: 13b043f3d6154852647f6bb738d3717be6802fa9
ms.sourcegitcommit: c87e036fe898318487ea8df31b13b328985ce0e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/19/2017
---
# <a name="install-and-configure-ansible-to-manage-virtual-machines-in-azure"></a>Установка и настройка Ansible для управления виртуальными машинами в Azure
В этой статье подробно описывается установка Ansible и необходимые модули Azure Python SDK для некоторых типичных дистрибутивы Linux. Чтобы установить Ansible в других дистрибутивах, настройте установленные пакеты в соответствии с платформой. Вы также узнаете, как создавать и определять учетные данные, используемые Ansible для безопасного создания ресурсов Azure. 

Сведения о дополнительных параметрах установки и инструкции для других платформ см. в [руководстве по установке Ansible](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Установка Ansible
Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). В следующем примере создается группа ресурсов с именем *myResourceGroupAnsible* в расположении *eastus*.

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Теперь создайте виртуальную Машину и установите Ansible для одного из следующих дистрибутивы по своему усмотрению.

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12 SP2](#sles-12-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). В приведенном ниже примере создается виртуальная машина с именем *myVMAnsible*.

```azurecli
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Подключитесь по SSH к виртуальной машине, используя адрес `publicIpAddress`, указанный в выходных данных операции по созданию виртуальной машины.

```bash
ssh azureuser@<publicIpAddress>
```

Установите в виртуальной машине необходимые пакеты модулей SDK для Azure Python и Ansible следующим образом:

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Ansible and Azure SDKs via pip
pip install ansible[azure]
```

Теперь перейдите к разделу [Создание учетных данных Azure](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). В приведенном ниже примере создается виртуальная машина с именем *myVMAnsible*.

```azurecli
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Подключитесь по SSH к виртуальной машине, используя адрес `publicIpAddress`, указанный в выходных данных операции по созданию виртуальной машины.

```bash
ssh azureuser@<publicIpAddress>
```

Установите в виртуальной машине необходимые пакеты модулей SDK для Azure Python и Ansible следующим образом:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Ansible and Azure SDKs via pip
sudo pip install ansible[azure]
```

Теперь перейдите к разделу [Создание учетных данных Azure](#create-azure-credentials).


### <a name="sles-12-sp2"></a>SLES 12 SP2
Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create). В приведенном ниже примере создается виртуальная машина с именем *myVMAnsible*.

```azurecli
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

Подключитесь по SSH к виртуальной машине, используя адрес `publicIpAddress`, указанный в выходных данных операции по созданию виртуальной машины.

```bash
ssh azureuser@<publicIpAddress>
```

Установите в виртуальной машине необходимые пакеты модулей SDK для Azure Python и Ansible следующим образом:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 make \
    python-devel libopenssl-devel libtool python-pip python-setuptools

## Install Ansible and Azure SDKs via pip
sudo pip install ansible[azure]

# Remove conflicting Python cryptography package
sudo pip uninstall -y cryptography
```

Теперь перейдите к разделу [Создание учетных данных Azure](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Создание учетных данных Azure
Ansible взаимодействует с Azure, используя имя пользователя и пароль или субъект-службу. Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Ansible. Вы можете управлять разрешениями на то, какие операции может выполнять субъект-служба в Azure, и определять их. Для обеспечения более высокого уровня безопасности, чем при предоставлении имени пользователя и пароля, в этом примере создается простейший субъект-служба.

Создание участника службы на главном компьютере с [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и учетные данные, необходимые для Ansible вывода:

```azurecli
az ad sp create-for-rbac --query [client_id: appId, secret: password, tenant: tenant]
```

Ниже приведен пример выходных данных предыдущей команды.

```json
{
  "client_id": "eec5624a-90f8-4386-8a87-02730b5410d5",
  "secret": "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47"
}
```

Для проверки подлинности в Azure также необходимо получить идентификатор подписки Azure с помощью команды [az account show](/cli/azure/account#show):

```azurecli
az account show --query "{ subscription_id: id }"
```

Выходные данные этих двух команд будут использоваться в следующем шаге.


## <a name="create-ansible-credentials-file"></a>Создание файла учетных данных Ansible
Чтобы предоставить учетные данные для Ansible, необходимо определить переменные среды или создать локальный файл учетных данных. Дополнительные сведения об определении учетных данных Ansible см. в разделе [предоставление учетных данных для модулей Azure](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

В среде разработки создайте файл *учетных данных* для Ansible в виртуальной машине узла следующим образом:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

В файле *учетных данных* объединяются идентификатор подписки и выходные данные, полученные в результате создания субъекта-службы. Выходные данные предыдущей [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) команда такая же, как это требуется для *client_id*, *секрет*, и *клиента*. В приведенном ниже примере файла *учетных данных* показаны значения, соответствующие выходным данным предыдущей команды. Введите свои значения следующим образом:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=eec5624a-90f8-4386-8a87-02730b5410d5
secret=531dcffa-3aff-4488-99bb-4816c395ea3f
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Использование переменных среды Ansible
Если вы собираетесь использовать такие средства, как Ansible Tower или Jenkins, можно определить переменные среды указанным ниже образом. В этих переменных объединяются идентификатор подписки и выходные данные, полученные в результате создания субъекта-службы. Выходные данные предыдущей команды [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) следуют в необходимом порядке: *AZURE_CLIENT_ID*, *AZURE_SECRET* и *AZURE_TENANT*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=eec5624a-90f8-4386-8a87-02730b5410d5
export AZURE_SECRET=531dcffa-3aff-4488-99bb-4816c395ea3f
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь Ansible и необходимые модули SDK для Azure Python установлены, а учетные данные для Ansible определены. Узнайте, как [создать виртуальную машину с Ansible](ansible-create-vm.md). Вы также можете узнать, как [создать готовую виртуальную машину Azure и вспомогательные ресурсы с помощью Ansible](ansible-create-complete-vm.md).
