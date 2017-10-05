---
title: "Установка MongoDB на виртуальную машину Linux с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как установить и настроить MongoDB на виртуальной машине Linux с помощью Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: e19c09558285497f29eb78b4f4ae5b15d7f1a191
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="46fb6-103">Как установить и настроить MongoDB на виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="46fb6-103">How to install and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="46fb6-104">[MongoDB](http://www.mongodb.org) — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="46fb6-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="46fb6-105">В этой статье показано, как установить и настроить MongoDB на виртуальной машине Linux с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="46fb6-105">This article shows you how to install and configure MongoDB on a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="46fb6-106">Эти действия можно также выполнить с помощью [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="46fb6-106">You can also perform these steps with the [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="46fb6-107">Изучив представленные примеры, вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="46fb6-107">Examples are shown that detail how to:</span></span>

* <span data-ttu-id="46fb6-108">[установить и настроить базовый экземпляр MongoDB вручную](#manually-install-and-configure-mongodb-on-a-vm);</span><span class="sxs-lookup"><span data-stu-id="46fb6-108">[Manually install and configure a basic MongoDB instance](#manually-install-and-configure-mongodb-on-a-vm)</span></span>
* <span data-ttu-id="46fb6-109">[создать базовый экземпляр MongoDB на основе шаблона Resource Manager](#create-basic-mongodb-instance-on-centos-using-a-template);</span><span class="sxs-lookup"><span data-stu-id="46fb6-109">[Create a basic MongoDB instance using a Resource Manager template](#create-basic-mongodb-instance-on-centos-using-a-template)</span></span>
* <span data-ttu-id="46fb6-110">[создать сложный сегментированный кластер MongoDB с набором реплик с использованием шаблона Resource Manager](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template).</span><span class="sxs-lookup"><span data-stu-id="46fb6-110">[Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="46fb6-111">Установка и настройка MongoDB на виртуальной машине вручную</span><span class="sxs-lookup"><span data-stu-id="46fb6-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="46fb6-112">База данных MongoDB [содержит инструкции по установке](https://docs.mongodb.com/manual/administration/install-on-linux/) для дистрибутивов Linux, в том числе Red Hat, CentOS, SUSE, Ubuntu и Debian.</span><span class="sxs-lookup"><span data-stu-id="46fb6-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="46fb6-113">В следующем примере создается виртуальная машина *CentOS*.</span><span class="sxs-lookup"><span data-stu-id="46fb6-113">The following example creates a *CentOS* VM.</span></span> <span data-ttu-id="46fb6-114">Для создания этой среды необходимо установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="46fb6-114">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="46fb6-115">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="46fb6-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="46fb6-116">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="46fb6-116">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="46fb6-117">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="46fb6-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="46fb6-118">В следующем примере создается виртуальная машина с именем *myVM* и именем пользователя *azureuser*, использующая аутентификацию с открытым ключом SSH.</span><span class="sxs-lookup"><span data-stu-id="46fb6-118">The following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="46fb6-119">Подключитесь к виртуальной машине по протоколу SSH с помощью имени пользователя и адреса `publicIpAddress`, указанного в результатах, полученных на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="46fb6-119">SSH to the VM using your own username and the `publicIpAddress` listed in the output from the previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="46fb6-120">Чтобы добавить источники установки для MongoDB, создайте файл репозитория **yum**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="46fb6-120">To add the installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="46fb6-121">Откройте файл репозитория MongoDB для редактирования.</span><span class="sxs-lookup"><span data-stu-id="46fb6-121">Open the MongoDB repo file for editing.</span></span> <span data-ttu-id="46fb6-122">Добавьте следующие строки.</span><span class="sxs-lookup"><span data-stu-id="46fb6-122">Add the following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="46fb6-123">Установите MongoDB, используя **yum**, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="46fb6-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="46fb6-124">По умолчанию в образах CentOS принудительно используется SELinux. Это препятствует доступу к MongoDB.</span><span class="sxs-lookup"><span data-stu-id="46fb6-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="46fb6-125">Установите средства управления политиками и настройте SELinux так, чтобы база данных MongoDB могла использовать TCP-порт 27017 по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="46fb6-125">Install policy management tools and configure SELinux to allow MongoDB to operate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="46fb6-126">Запустите службу MongoDB следующим образом:</span><span class="sxs-lookup"><span data-stu-id="46fb6-126">Start the MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="46fb6-127">Проверьте установленную базы данных MongoDB, подключившись к ней с помощью локального клиента `mongo`:</span><span class="sxs-lookup"><span data-stu-id="46fb6-127">Verify the MongoDB installation by connecting using the local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="46fb6-128">Теперь проверьте экземпляр MongoDB, добавив некоторые данные и выполнив их поиск:</span><span class="sxs-lookup"><span data-stu-id="46fb6-128">Now test the MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="46fb6-129">При необходимости настройте автоматический запуск MongoDB при перезагрузке системы:</span><span class="sxs-lookup"><span data-stu-id="46fb6-129">If desired, configure MongoDB to start automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="46fb6-130">Создание базового экземпляра MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="46fb6-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="46fb6-131">На виртуальной машине CentOS можно создать базовый экземпляр MongoDB, используя следующий шаблон быстрого запуска Azure из GitHub.</span><span class="sxs-lookup"><span data-stu-id="46fb6-131">You can create a basic MongoDB instance on a single CentOS VM using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="46fb6-132">В этом шаблоне используется расширение настраиваемых скриптов для Linux, что позволяет добавить в созданную виртуальную машину CentOS репозиторий **yum**, а затем установить MongoDB.</span><span class="sxs-lookup"><span data-stu-id="46fb6-132">This template uses the Custom Script extension for Linux to add a **yum** repository to your newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="46fb6-133">[Базовый экземпляр MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="46fb6-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="46fb6-134">Для создания этой среды необходимо установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="46fb6-134">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="46fb6-135">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="46fb6-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="46fb6-136">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="46fb6-136">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="46fb6-137">Затем разверните шаблон MongoDB с помощью команды [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="46fb6-137">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="46fb6-138">Определите необходимые имена и размеры ресурсов, например *newStorageAccountName*, *virtualNetworkName* и *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="46fb6-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

<span data-ttu-id="46fb6-139">Войдите на виртуальную машину с помощью ее общедоступного DNS-адреса.</span><span class="sxs-lookup"><span data-stu-id="46fb6-139">Log on to the VM using the public DNS address of your VM.</span></span> <span data-ttu-id="46fb6-140">Его можно просмотреть с помощью команды [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="46fb6-140">You can view the public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="46fb6-141">Подключитесь к виртуальной машине по протоколу SSH с помощью имени пользователя и общедоступного DNS-адреса.</span><span class="sxs-lookup"><span data-stu-id="46fb6-141">SSH to your VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="46fb6-142">Проверьте установку базы данных MongoDB, подключившись к ней с помощью локального клиента `mongo`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="46fb6-142">Verify the MongoDB installation by connecting using the local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="46fb6-143">Теперь проверьте экземпляр, добавив некоторые данные и выполнив их поиск, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="46fb6-143">Now test the instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="46fb6-144">Создание сложного сегментированного кластера MongoDB на виртуальной машине CentOS с использованием шаблона</span><span class="sxs-lookup"><span data-stu-id="46fb6-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="46fb6-145">Используя следующий шаблон быстрого запуска Azure из GitHub, можно создать сложный сегментированный кластер MongoDB.</span><span class="sxs-lookup"><span data-stu-id="46fb6-145">You can create a complex MongoDB sharded cluster using the following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="46fb6-146">Этот шаблон соответствует [рекомендациям для сегментированного кластера MongoDB](https://docs.mongodb.com/manual/core/sharded-cluster-components/) в отношении избыточности и высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="46fb6-146">This template follows the [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) to provide redundancy and high availability.</span></span> <span data-ttu-id="46fb6-147">Он предусматривает создание двух сегментов с тремя узлами в каждом наборе реплик.</span><span class="sxs-lookup"><span data-stu-id="46fb6-147">The template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="46fb6-148">Кроме того, он создает набор реплик сервера конфигурации и два сервера маршрутизации **mongos**. Это позволяет обеспечить согласованность приложений из разных сегментов.</span><span class="sxs-lookup"><span data-stu-id="46fb6-148">One config server replica set with three nodes is also created, plus two **mongos** router servers to provide consistency to applications from across the shards.</span></span>

* <span data-ttu-id="46fb6-149">[Сегментированный кластер MongoDB на виртуальной машине CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos): https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="46fb6-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="46fb6-150">Для развертывания сложного сегментированного кластера MongoDB требуется более 20 ядер. Обычно 20 ядер — это количество по умолчанию для региона, выделяемое на одну подписку.</span><span class="sxs-lookup"><span data-stu-id="46fb6-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically the default core count per region for a subscription.</span></span> <span data-ttu-id="46fb6-151">Отправьте запрос в службу поддержки Azure, чтобы увеличить количество ядер.</span><span class="sxs-lookup"><span data-stu-id="46fb6-151">Open an Azure support request to increase your core count.</span></span>

<span data-ttu-id="46fb6-152">Для создания этой среды необходимо установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="46fb6-152">To create this environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="46fb6-153">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="46fb6-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="46fb6-154">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="46fb6-154">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="46fb6-155">Затем разверните шаблон MongoDB с помощью команды [az group deployment create](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="46fb6-155">Next, deploy the MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="46fb6-156">Определите необходимые имена и размеры ресурсов, например *mongoAdminUsername*, *sizeOfDataDiskInGB* и *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="46fb6-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

<span data-ttu-id="46fb6-157">На то, чтобы развернуть и настроить все экземпляры виртуальной машины, может потребоваться более одного часа.</span><span class="sxs-lookup"><span data-stu-id="46fb6-157">This deployment can take over an hour to deploy and configure all the VM instances.</span></span> <span data-ttu-id="46fb6-158">Флаг `--no-wait` в конце предыдущей команды используется для возвращения управления командной строке после того, как развертывание шаблона будет принято платформой Azure.</span><span class="sxs-lookup"><span data-stu-id="46fb6-158">The `--no-wait` flag is used at the end of the preceding command to return control to the command prompt once the template deployment has been accepted by the Azure platform.</span></span> <span data-ttu-id="46fb6-159">Затем можно просмотреть состояние развернутой службы с помощью команды [az group deployment show](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="46fb6-159">You can then view the deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="46fb6-160">Приведенный ниже пример позволяет просмотреть состояние развернутой службы *myMongoDBCluster* в группе ресурсов *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="46fb6-160">The following example views the status for the *myMongoDBCluster* deployment in the *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="46fb6-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46fb6-161">Next steps</span></span>
<span data-ttu-id="46fb6-162">В этих примерах подключение к экземпляру MongoDB выполняется локально с помощью виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="46fb6-162">In these examples, you connect to the MongoDB instance locally from the VM.</span></span> <span data-ttu-id="46fb6-163">Чтобы подключится к экземпляру MongoDB из другой виртуальной машины или сети, [создайте соответствующие правила группы безопасности сети](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="46fb6-163">If you want to connect to the MongoDB instance from another VM or network, ensure the appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="46fb6-164">В этих примерах в целях разработки развертывается основная среда MongoDB.</span><span class="sxs-lookup"><span data-stu-id="46fb6-164">These examples deploy the core MongoDB environment for development purposes.</span></span> <span data-ttu-id="46fb6-165">Примените необходимые параметры конфигурации безопасности для среды.</span><span class="sxs-lookup"><span data-stu-id="46fb6-165">Apply the required security configuration options for your environment.</span></span> <span data-ttu-id="46fb6-166">Дополнительные сведения о безопасности MongoDB см. на [этой странице](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="46fb6-166">For more information, see the [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="46fb6-167">Дополнительные сведения о создании с использованием шаблонов см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46fb6-167">For more information about creating using templates, see the [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="46fb6-168">Для скачивания и выполнения скриптов на виртуальных машинах в шаблонах Azure Resource Manager используется расширение настраиваемых скриптов.</span><span class="sxs-lookup"><span data-stu-id="46fb6-168">The Azure Resource Manager templates use the Custom Script Extension to download and execute scripts on your VMs.</span></span> <span data-ttu-id="46fb6-169">Дополнительные сведения см. в статье [Использование расширения пользовательских сценариев Azure на виртуальных машинах Linux](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="46fb6-169">For more information, see [Using the Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

