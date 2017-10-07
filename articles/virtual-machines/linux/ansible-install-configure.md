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
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="2de30-103">Установка и настройка Ansible toomanage виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="2de30-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="2de30-104">В этой статье указаны hello как tooinstall Ansible и необходимые модули Azure Python SDK, для некоторых типичных дистрибутивы Linux.</span><span class="sxs-lookup"><span data-stu-id="2de30-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="2de30-105">Можно установить Ansible на других дистрибутивах перемещая hello установлены пакеты toofit вашей конкретной платформы.</span><span class="sxs-lookup"><span data-stu-id="2de30-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="2de30-106">toocreate Azure ресурсы в безопасном режиме, вы также узнаете, как toocreate и укажите учетные данные для Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="2de30-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="2de30-107">Дополнительные параметры установки и шаги для дополнительных платформ см. в разделе hello [Ansible руководство по установке](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="2de30-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="2de30-108">Установка Ansible</span><span class="sxs-lookup"><span data-stu-id="2de30-108">Install Ansible</span></span>
<span data-ttu-id="2de30-109">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2de30-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2de30-110">Hello следующий пример создает группу ресурсов с именем *myResourceGroupAnsible* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="2de30-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="2de30-111">Теперь создайте виртуальную Машину и установите Ansible для одного из следующих дистрибутивы hello.</span><span class="sxs-lookup"><span data-stu-id="2de30-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="2de30-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2de30-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="2de30-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="2de30-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="2de30-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="2de30-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="2de30-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="2de30-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="2de30-116">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2de30-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2de30-117">Hello следующий пример создает Виртуальную машину с именем *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="2de30-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2de30-118">SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` нижеприведенного hello операции создания вывод hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="2de30-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2de30-119">На ВМ установите hello необходимые пакеты для модулей Azure Python SDK hello и Ansible следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2de30-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

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

<span data-ttu-id="2de30-120">Теперь перейдем слишком[учетные данные Azure создать](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="2de30-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="2de30-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="2de30-121">CentOS 7.3</span></span>
<span data-ttu-id="2de30-122">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2de30-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2de30-123">Hello следующий пример создает Виртуальную машину с именем *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="2de30-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2de30-124">SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` нижеприведенного hello операции создания вывод hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="2de30-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2de30-125">На ВМ установите hello необходимые пакеты для модулей Azure Python SDK hello и Ansible следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2de30-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="2de30-126">Теперь перейдем слишком[учетные данные Azure создать](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="2de30-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="2de30-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="2de30-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="2de30-128">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2de30-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2de30-129">Hello следующий пример создает Виртуальную машину с именем *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="2de30-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2de30-130">SSH tooyour виртуальной Машины с помощью hello `publicIpAddress` нижеприведенного hello операции создания вывод hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="2de30-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2de30-131">На ВМ установите hello необходимые пакеты для модулей Azure Python SDK hello и Ansible следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2de30-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="2de30-132">Теперь перейдем слишком[учетные данные Azure создать](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="2de30-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="2de30-133">Создание учетных данных Azure</span><span class="sxs-lookup"><span data-stu-id="2de30-133">Create Azure credentials</span></span>
<span data-ttu-id="2de30-134">Ansible взаимодействует с Azure, используя имя пользователя и пароль или субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="2de30-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="2de30-135">Субъект-служба Azure является удостоверением безопасности, которое можно использовать с приложениями, службами и средствами автоматизации, такими как Ansible.</span><span class="sxs-lookup"><span data-stu-id="2de30-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="2de30-136">Управление и определить hello разрешения участника службы hello toowhat операции можно выполнять в Azure.</span><span class="sxs-lookup"><span data-stu-id="2de30-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="2de30-137">безопасность tooimprove просто задать имя пользователя и пароль, этот пример создает базовую службу участника.</span><span class="sxs-lookup"><span data-stu-id="2de30-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="2de30-138">Создание службы с основной [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) и hello учетные данные, которые требуется Ansible выходные данные:</span><span class="sxs-lookup"><span data-stu-id="2de30-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="2de30-139">Пример выходных данных hello hello предшествующий команды выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2de30-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="2de30-140">tooauthenticate tooAzure, необходимо также идентификатор подписки Azure с tooobtain [az учетной записи, отображают](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="2de30-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="2de30-141">В следующем шаге hello используйте hello выходные данные этих двух команд.</span><span class="sxs-lookup"><span data-stu-id="2de30-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="2de30-142">Создание файла учетных данных Ansible</span><span class="sxs-lookup"><span data-stu-id="2de30-142">Create Ansible credentials file</span></span>
<span data-ttu-id="2de30-143">tooprovide учетные данные tooAnsible, определения переменных среды или создать файл локальные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2de30-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="2de30-144">Дополнительные сведения о том, как toodefine Ansible учетные данные, в разделе [tooAzure учетные данные, предоставляя модулей](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="2de30-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="2de30-145">В среде разработки создайте файл *учетных данных* для Ansible в виртуальной машине узла следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2de30-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="2de30-146">Hello *учетные данные* сам файл объединяет hello идентификатор подписки с выводом hello создания участника службы.</span><span class="sxs-lookup"><span data-stu-id="2de30-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="2de30-147">Выходные данные предыдущей hello [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) команда является таким же hello заказа, необходимые для *client_id*, *секрет*, и *клиента* .</span><span class="sxs-lookup"><span data-stu-id="2de30-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="2de30-148">Следующий пример Hello *учетные данные* файле отображаются эти значения соответствия hello предыдущие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2de30-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="2de30-149">Введите свои значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2de30-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="2de30-150">Использование переменных среды Ansible</span><span class="sxs-lookup"><span data-stu-id="2de30-150">Use Ansible environment variables</span></span>
<span data-ttu-id="2de30-151">Если вы собираетесь toouse средств, таких как Ansible Tower или Jenkins, переменные среды можно определить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2de30-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="2de30-152">Эти переменные объединять hello идентификатор подписки с результатом hello создания участника службы.</span><span class="sxs-lookup"><span data-stu-id="2de30-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="2de30-153">Выходные данные предыдущей hello [az ad sp создать для rbac](/cli/azure/ad/sp#create-for-rbac) команда является таким же hello заказа, необходимые для *AZURE_CLIENT_ID*, *AZURE_SECRET*, и *AZURE_ КЛИЕНТ*.</span><span class="sxs-lookup"><span data-stu-id="2de30-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="2de30-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2de30-154">Next steps</span></span>
<span data-ttu-id="2de30-155">Теперь у вас есть Ansible и hello необходимые модули Azure Python SDK, а учетные данные, определенные для Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="2de30-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="2de30-156">Узнайте, каким образом слишком[Создание ВМ с Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2de30-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="2de30-157">Также вы можете узнать, каким образом слишком[создания завершения виртуальной Машины Azure и поддержку ресурсов с Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2de30-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
